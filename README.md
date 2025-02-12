# langGraphs-Utils
Repo for details LangGraph Concepts

# Checkpointers while using Sub-Graphs or Multi-Agent Graph
#### Problem Statement: 
In case of multiple Graphs or Sub-graphs in my app, how to handle and declare the checkpointers efficiently.

#### Solution:
Key Principles for Checkpointing Nested Graphs: 
• You should only initialize ONE checkpointer for the parent/top-level graph 
• Do NOT initialize separate checkpointers for subgraphs 
• The parent graph's checkpointer will automatically be propagated to all nested subgraphs

```python
from langgraph.graph import StateGraph
from langgraph.checkpoint.memory import MemorySaver

# Initialize a single checkpointer for the entire graph hierarchy
checkpointer = MemorySaver()

# Parent graph compilation automatically handles subgraph checkpointing
grandparent_graph = grandparent_graph.compile(checkpointer=checkpointer)

```

###### Proof Points from Documentation: 
• LangGraph explicitly states: "You shouldn't provide a checkpointer when compiling a subgraph"
• The checkpointer is automatically propagated to child graphs when you compile the parent graph 
• This approach ensures consistent state tracking across nested graph structures

Verification Example:
```python
# When running a nested graph, you can inspect states at different levels
state = grandparent_graph.get_state(config, subgraphs=True)
print("Grandparent State:", state.values)
print("Parent Graph State:", state.tasks[[0]](https://docs.smith.langchain.com/evaluation/how_to_guides/langgraph).state.values)
print("Subgraph State:", state.tasks[[0]](https://docs.smith.langchain.com/evaluation/how_to_guides/langgraph).state.tasks[[0]](https://docs.smith.langchain.com/evaluation/how_to_guides/langgraph).state.values)

```

###### Recommendation: Always use a single checkpointer initialized at the top-level graph compilation.
