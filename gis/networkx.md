### determining the shortest path length

### introduction
```py
import networkx as nx
G = nx.Graph() # build an empty graph
```
### adding edges
```
G.add_edge("<A>", "<B>", weight = , relation = "") # add an edge between nodes A and B,
G.edges(data=True)
```

### adding nodes
```py
G.add_node("<A>", role = "") # creates a node with attribute *role*
G.edges(data=True)
```

### visualizing the graph
- `nx.draw_networkx(G, with_labels= True)`


### bipartite graph (like match-the-following)
```py
B = nx.Graph()
B.add_nodes_from(["A", "B", "C", "D", "E"], bipartite = 0)
B.add_nodes_from([1,2,3,4], bipartite= 1)
B= add_edges_from([("A", 1),("B", 1), ("C", 1), ("C", 3), ("D", 4), ("E", 1), ("A", 2), ("E", 2) ])
bipartite.is_bipartite(B)
```

### example


### loading dataset 
```py
import csv
from operator import itemgetter

nodes =  # list of list, [nodeid, attribute1, attribute2, attribute3]
edges = # list of edges. eg. (A, 1), (B,3)

G = nx.Graph()

G.add_nodes_from(nodes)
G.add_edges_from(edges)

print(nx.info(G))

```
### adding attributes
```py 
nx.set_node_attributes(G, dict_1, "name_of_attribute")
```

### density
```
density = nx.density(G)
```


### calculating shortest path
```
path = nx.shortest_path(G, source = "", target="")
``` 
