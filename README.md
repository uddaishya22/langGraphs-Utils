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

###### Proof Points from Documentation: 
• LangGraph explicitly states: "You shouldn't provide a checkpointer when compiling a subgraph"
• The checkpointer is automatically propagated to child graphs when you compile the parent graph 
• This approach ensures consistent state tracking across nested graph structures

###### Recommendation: Always use a single checkpointer initialized at the top-level graph compilation.
