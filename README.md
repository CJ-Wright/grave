<div align="center">
    <table border=0>
        <tr>
            <td>
                <h1> grave </h1>
                <a href="https://travis-ci.org/networkx/grave">
                    <img src="https://travis-ci.org/networkx/grave.svg?branch=master"><br>
                </a>
                <a href='http://grave.readthedocs.io/en/latest/?badge=latest'>
                    <img src='http://readthedocs.org/projects/grave/badge/?version=latest' alt='Documentation Status'>
                </a>   
            </td>
            <td align="center">
                <img src="https://github.com/networkx/grave/raw/master/doc/default.png" width=50%><br>
            </td>
        </tr>
    </table>
</div>

GraVE is a Graph Visualization Package combining ideas from
Matplotlib, NetworkX, and seaborn. Its goal is to provide a
network drawing API that covers the most use cases with sensible
defaults and simple style configuration. Currently, it supports
drawing graphs from NetworkX.

## Example Usage

Here, we create a graph and color the nodes in its minimum weighted dominating set:

```python
import matplotlib.pyplot as plt
import networkx as nx
from networkx.algorithms.approximation.dominating_set import min_weighted_dominating_set

from grave import plot_network

network = nx.barbell_graph(10, 10)
dom_set = min_weighted_dominating_set(network)

for node, node_attrs in network.nodes(data=True):
    node_attrs['is_dominator'] = True if node in dom_set else False

def color_dominators(node_attrs):
    if node_attrs.get('is_dominator', False):
        return {'color': 'red'}
    else:
        return {'color': 'gray'}

fig, ax = plt.subplots()
plot_network(network, node_style=color_dominators)
plt.show()

```

The result:

<div align="center">
    <img src="https://github.com/networkx/grave/raw/master/doc/dominators.png" width=75%>
</div>
