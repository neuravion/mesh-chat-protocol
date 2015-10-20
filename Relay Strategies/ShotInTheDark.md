# The Shot in the Dark Strategy
This is a non-optimal strategy which does not require the mesh network graph to be held in memory.

## The Algorithm
1. The initial sender (hereafter known as **Origin**) wants to send to a specific node (hereafter known as **Target**)
2. **Origin** checks if **Target** is an immediate family connection
  * If **Target** is a connection, it is sent directly and we exit the workflow
3. **Origin** sends to one of its immediate family connections along with the following information
  * `sequence`: The sequence of node jumps which have occurred up until now
  * `visited`: All nodes which have been visited thus far
4. A connection receives the message from **Origin** along with the information, then...
  * It adds itself to both `sequence` and `visited`
  * The process begins again at 2, but connections are limited to nodes which do not appear in `visited`
5. If no nodes are available to the connection which are not currently in `visited`, the process is disjointed and sent back to the previous sender, who maintains the state of `visited`

## Advantages
* Does not require a built graph structure on the client
* Works extremely well with small networks that don't contain a nodes that need relays
* Can handle non-clientized disconnects without much issue

## Disadvantages
* Worst case scenario, every node in the graph will be visited. 
* It is up to each node to keep track of success rates in communicating to other nodes
