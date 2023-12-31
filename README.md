# bfs_using_python
Breath_First_Search in which the root node is expanded first then all the successor of the root node are expanded next, f(n)-depth of the node, no. of actions it takes to reach the node. FIFO first in first out early goal test, BFS finds sol of minimal no. of action generation nodes of depth d.
import networkx as nx
import matplotlib.pyplot as plt
from collections import deque

# Create a sample graph
G = nx.Graph()
G.add_edges_from([(0, 1), (0, 2), (1, 3), (1, 4), (2, 5), (2, 6)])

# Initialize BFS
start_node = 0
visited = set()
queue = deque()
queue.append(start_node)
visited.add(start_node)

# Create a figure for visualization
plt.figure(figsize=(8, 6))

while queue:
    current_node = queue.popleft()
    neighbors = list(G.neighbors(current_node))

    for neighbor in neighbors:
        if neighbor not in visited:
            visited.add(neighbor)
            queue.append(neighbor)

            # Visualization: Draw the current state of the graph
            plt.clf()
            pos = nx.spring_layout(G, seed=42)
            nx.draw(G, pos, with_labels=True, node_color='lightblue', font_size=12, node_size=500)
            nx.draw_networkx_nodes(G, pos, nodelist=[current_node], node_color='red', node_size=500)
            nx.draw_networkx_edges(G, pos, edgelist=[(current_node, neighbor)], edge_color='red', width=2)
            plt.title(f'BFS: Visiting Node {current_node}')
            plt.pause(1)  # Pause for visualization (1 second)

# Final visualization
plt.clf()
pos = nx.spring_layout(G, seed=42)
nx.draw(G, pos, with_labels=True, node_color='lightblue', font_size=12, node_size=500)
plt.title('BFS: Final State')
plt.show()
