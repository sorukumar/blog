---
layout: post
title: "How many Nodes & How many Channels - Reconciliation of number"
categories: Lightning Technical
author:
- sorukumar
---

This is a post to help develop an informed opinion on how many nodes and channels we have in the Lightning network.

We'll look at Amboss, 1ml, Mempool, hashXP data, and then at the graph output from an LND node. [The graph output](https://lightning.engineering/api-docs/api/lnd/lightning/describe-graph) has info on nodes and channels.


## 6-15K nodes and 50-60K channels

[Data](https://amboss.space/stats?params=eyJtZXRyaWMiOiJhY3RpdmVfbm9kZXMiLCJjYXRlZ29yeSI6ImFsbFRpbWVNZXRyaWNzIn0=) on 04/03/2024
 - Amboss: Nodes ~16K, Channel ~58K
 - [1ml](https://1ml.com/): Nodes ~14K, Channels ~52K
 - Mempool: Nodes ~13K, Channel ~52K
 - [hashXP](https://hashxp.org/lightning/node/): ~6k live nodes, and 16k zombie nodes

Hashxp talks about zombie nodes. What exactly is it? Are we okay with the definition of zombie nodes? Or the better approach would be to understand the approach and use and talk about a number based on context.

## Analyzing LND output 
The output json file has two data components. One is for nodes and another one is for channels. A basic data pull shows:

| Description    | Count  |
|--|--|
| # of Nodes     | 15246  |
| # of Channels  | 51861  |


The output from my nodes is closest to 1ml and Mempool. We'll continue slicing and dicing our data to understand it more, and hopefully, it will give us some understanding to make sense of data in other explorers. 

## Slicing the nodes' data

The node data has below columns

Code:

    first_node = graph_data['nodes'][0]  # Get the first item (node)
    node_keys = first_node.keys()  # Get the keys, which represent the columns
    print("Columns in 'nodes' dictionary:", node_keys)

Output:

> Columns in 'nodes' dictionary: dict_keys(['last_update', 'pub_key', 'alias', 'addresses', 'color', 'features', 'custom_records'])

Are all pub keys ( node ID) unique here?

Code

    print("Count of unique pub_keys:", len({node['pub_key'] for node in graph_data['nodes']}))

Output:

> Count of unique pub_keys: 15246

This is the number of nodes that I said earlier, we got from the 'describegraph' output from my node. Now, can we trim out zombie nodes -- nodes that are 'dead'.

Lets look at how many nodes have never sent an update of their presence to their peer for broadcasting.

Code:

   
    count_last_update_greater_than_0 = 0
    count_last_update_less_or_equal_0 = 0
    for node in graph_data['nodes']:
        if node['last_update'] > 0:
            count_last_update_greater_than_0 += 1
        else:
            count_last_update_less_or_equal_0 += 1>
        print(f"Count of pub_keys with last_update > 0: {count_last_update_greater_than_0}")
        print(f"Count of pub_keys with last_update <= 0:{count_last_update_less_or_equal_0}")

Output:

> Count of pub_keys with last_update > 0: 9321
Count of pub_keys with last_update <= 0: 5925

~6K Nodes have never broadcasted their presence. They could be zombie nodes. Based on this work, we have 9k nodes to work with. However, hashXP thinks that there are still some zombies hiding in 9k. We'll need to get to edges (Channels) data to find them out.



## Slicing the edges/channel data

The channel data has below columns

Code:

    first_edges = graph_data['edges'][0]  
    edges_keys = first_edges.keys() 
    print("Columns in 'edges' dictionary:", edges_keys)

Output:

>Columns in 'edges' dictionary: dict_keys(['channel_id', 'chan_point', 'last_update', 'node1_pub', 'node2_pub', 'capacity', 'node1_policy', 'node2_policy', 'custom_records'])

Edges are unique on channel_id. Remember, two nodes may have multiple channels between them. Let's find out  how many channels have never been updated.

Code:
   
    count_last_update_greater_than_0 = 0
    count_last_update_less_or_equal_0 = 0
    
    for edges in graph_data['edges']:
        if edges['last_update'] > 0:
            count_last_update_greater_than_0 += 1
        else:
            count_last_update_less_or_equal_0 += 1
    
    print(f"Count of channels with last_update > 0: {count_last_update_greater_than_0}")
    print(f"Count of channels with last_update <= 0: {count_last_update_less_or_equal_0}")

Output:

> Count of channels with last_update > 0: 37166
Count of channels with last_update <= 0: 14695

~15k channels out of ~52K channels that we got querying our node have never been updated. Most likely, they are not usable and are zombies, but let's continue looking at more variables. We'll look at capacity/channel size now.

Code:
   

    count_capacity_greater_than_0 = 0
    count_capacity_less_or_equal_0 = 0
    
    for edges in graph_data['edges']:
        if int(edges['capacity']) > 0:
            count_capacity_greater_than_0 += 1
        else:
            count_capacity_less_or_equal_0 += 1
    
    print(f"Count of channels with capacity > 0: {count_capacity_greater_than_0}")
    print(f"Count of channels with capacity <= 0: {count_capacity_less_or_equal_0}")

Output:

> Count of channels with capacity > 0: 37915
Count of channels with capacity <= 0: 13946

~14k channels have no capacity. These channels are not usable at all without any doubt. But how do 14k channels with no capacity overlap with 15k channels that have not sent any updates?

| Group # | Group based on Last update, Capacity, and node policy data |# of channels |
|--|--|--|
| 1 | last update > 0, capacity > 0, Both policies are good - non-null |37067 |
| 2 | last update = 0, capacity = 0, Both are null | 13915|
| 3 | last update = 0, capacity > 0, Both are null |780 |
| 4 | last update > 0, capacity > 0, One policy is null | 68|
| 5 | last update > 0, capacity = 0, Both policies are good - non-null |28 |
| 6 | last update > 0, capacity = 0, One policy is null |3 |

From the above work, it seems not more than 37k to 38k channels are usable. But how many of these usable channels are from so-called 'zombie' nodes of node data? Or, is it possible that out of ~9k nodes that have sent an update a good percentage don't have a usable channel?

## Cross tabulating Nodes and Channel Data


'Source node last update' or 'target node last update' is the last update from node data for the source node or target node. The 'last update' comes from channel data, and it is the last update for the channel. Capacity and policy fields are of course channel-specific data.

We got a unique pub key count. it is unique only for a group. Considering some fields of the group are made up of channel data. 'Unique pub key count' counts unique pub key for both  source or target pub key.

| Group Number | Group                                                                                                      | Count | Unique Pub Key Count |
|--------------|------------------------------------------------------------------------------------------------------------|-------|----------------------|
| 1            | source node last update > 0, target node last update > 0, last update > 0, capacity > 0, Both policies are non-null | 36999 | 7899                 |
| 2            | source node last update <= 0, target node last update <= 0, last update <= 0, capacity <= 0, Both policies are null  | 4380  | 3244                 |
| 3            | source node last update <= 0, target node last update > 0, last update <= 0, capacity <= 0, Both policies are null   | 3795  | 2953                 |
| 4            | source node last update > 0, target node last update <= 0, last update <= 0, capacity <= 0, Both policies are null   | 3357  | 2668                 |
| 5            | source node last update > 0, target node last update > 0, last update <= 0, capacity <= 0, Both policies are null   | 2383  | 1340                 |
| 6            | source node last update <= 0, target node last update > 0, last update <= 0, capacity > 0, Both policies are null    | 271   | 343                  |
| 7            | source node last update > 0, target node last update > 0, last update <= 0, capacity > 0, Both policies are null     | 199   | 262                  |
| 8            | source node last update <= 0, target node last update <= 0, last update <= 0, capacity > 0, Both policies are null   | 163   | 266                  |
| 9            | source node last update > 0, target node last update <= 0, last update <= 0, capacity > 0, Both policies are null    | 147   | 218                  |
| 10           | source node last update > 0, target node last update > 0, last update > 0, capacity > 0, One policy is null          | 49    | 86                   |
| 11           | source node last update > 0, target node last update <= 0, last update > 0, capacity > 0, Both policies are non-null | 46    | 61                   |
| 12           | source node last update > 0, target node last update > 0, last update > 0, capacity <= 0, Both policies are non-null | 28    | 28                   |
| 13           | source node last update <= 0, target node last update > 0, last update > 0, capacity > 0, Both policies are non-null | 22    | 31                   |
| 14           | source node last update > 0, target node last update <= 0, last update > 0, capacity > 0, One policy is null         | 13    | 22                   |
| 15           | source node last update <= 0, target node last update > 0, last update > 0, capacity > 0, One policy is null         | 6     | 11                   |
| 16           | source node last update > 0, target node last update > 0, last update > 0, capacity <= 0, One policy is null         | 2     | 4                    |
| 17           | source node last update > 0, target node last update <= 0, last update > 0, capacity <= 0, One policy is null        | 1     | 2                    |


From the above table, the 7.8k node looks good to go. We can consider them active nodes. Make a note of group 5. These nodes have updates on nodes, but we have 2.3k channels from them that have no update.


## Putting it all together

Based on our work, we can say 7.8K nodes are active. One of the explorer hashXP says only 6k nodes are active, we are still 1.8k ahead. Remember, our filtering criterion is last update > 0, so a node or a channel that has no update in the last year is counted as active. Does it make sense to do it? We will discuss it in next post.

## Notes

 
 - Mismatch in the data for count of nodes and channels in different lightning network explorers are mostly because of how they define nodes and active nodes. Different nodes seeing different views of the lightning graph is not the primary reason.
 - No one sees private channels/nodes, except private channels that are connected to them. So, it is not getting counted anywhere.
 - We can call inactive nodes zombie nodes, but quite likely some of them rise from the dead and send a transaction or two, and then go to sleep again. There may be reactivation of nodes. I'll talk about it later.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyMzE5MTcwOCw1NTcxNDU3NTksLTg3MD
Y2MDU0Nl19
-->