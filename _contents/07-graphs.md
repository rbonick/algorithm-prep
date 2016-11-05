---
title: Graphs
---

## Graphs
Graphs are similar to trees, except there is no hierarchy.
```
class GraphNode {
    int value;
    List<GraphNode> adjacent;
}
```

###### Depth First Search
```
void depthFirstSearch(GraphNode root){
    if(root == null){
        return;
    }
    visit(root);
    root.visited = true;
    for(GraphNode node : root.adjacent){
        if(node.visited == false){
            depthFirstSearch(node);
        }
    }
}
```

###### Breadth First Search
Important part of BFS is to use a Queue.
```
void breadthFirstSearch(GraphNode node){
    Queue queue = new Queue();
    root.visited = true;
    visit(root);
    queue.enqueue(root);

    while(!queue.isEmpty()){
        GraphNode currentNode = queue.dequeue();
        for(GraphNode node : currentNode.adjacent){
            if(!node.visited){
                visit(node);
                node.visited = true;
                queue.enqueue(node);
            }
        }
    }
}
```
