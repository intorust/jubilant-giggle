# Vector and indices

The "vector and index" pattern is a very simple way to model virtually any kind of data structure, particularly those with cycles or other shapes that don't fit Rust's .

## Short description

* For each node, create two types
    * A `struct Node(usize)` representing references to a node via a vector index
    * A `struct NodeData { ..., link: Node }` representing the data in a node
* Store your graph `struct Graph { nodes: Vec<NodeData> }` with
    * accessors for node data
        * `fn edge(&self, node: Node) -> &NodeData { &self.nodes[node.0] }`
        * `fn edge_mut(&mut self, node: Node) -> &mut NodeData { &mut self.nodes[node.0] }`

## When it works well

* When you mainly *add* things to your graph, not remove them
* When you want to share your graph in a read-only fashion across threads, but be able to mutate it when not shared

## When it works less well

* You have a long-lived graph where you will be adding and removing nodes over time
    * Because 

## Alternatives and ways to make it safer

* [Newtyped indices](./newtyped_indices.md)

## References

### Crates

* [petgraph](https://crates.io/crates/petgraph)

### Real-world examples of this pattern in use

### Blog posts

* [Modeling graphs in Rust using Vector indices](https://smallcultfollowing.com/babysteps/blog/2015/04/06/modeling-graphs-in-rust-using-vector-indices/)



