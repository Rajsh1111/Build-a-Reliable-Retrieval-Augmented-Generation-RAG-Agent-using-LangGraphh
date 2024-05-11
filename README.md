# Build-a-Reliable-Retrieval-Augmented-Generation-RAG-Agent-using-LangGraphh
Here we will build reliable RAG agents using LangGraph, Groq-Llama-3 and Chroma, We will combine the below concepts to build the RAG Agent.

![RAG Agent Workflow](C:/Users/rajee/OneDrive/Pictures/RAG.png)


Adaptive RAG (paper). We have implemented the concept to build a Router for routing questions to different retrieval approaches
Corrective RAG (paper). We have implemented the concept  to develop a fallback mechanism to progress with when the context retrieved is irrelevant to the question asked.
Self-RAG (paper). We have implemented the concept  to develop a hallucination grader .i.e. fix answers that hallucinate or doesn’t address the question asked.

**What is an Agent ?**
The fundamental concept behind agents involves employing a language model to select a sequence of actions. While in chains, this sequence is hardcoded within the code. Conversely, agents utilize a language model as a reasoning engine to decide the actions to take and their order.

It comprises of 3 components:

planning : breaking tasks into smaller sub-goals
memory : short term(chat history) / long term(vectorstore)
Tool Use : It can make uise of different tools to extend it’s capabilities.
Agents can me manifested by using ReAct concept with Langchain or by using LangGraph,

**Tradeoffs between Langchain Agent and LangGraph:**

Reliability:

ReAct / Langchain Agent: Less Reliable as LLM has to make the correct decision at each step
LangGraph : More Reliable as control flow is set and LLM has a specific job to perform at each node

Flexibility:

ReAct /Langchain Agent : More Flexible as LLM can choose any sequence of actions
LangGraph : Less Flexible as actions is constrained by setting up the control flow at each node
Compatibility with smaller LLMs

ReAct /Langchain Agent : Worse Compatibility
LangGraph : Better Compatibility
Here we have used LangGraph to create the Agent.

🦜️🔗 What is Langchain ?
LangChain is a framework for developing applications powered by language models. It enables applications that:

Are context-aware: connect a language model to sources of context (prompt instructions, few shot examples, content to ground its response in, etc.)
Reason: rely on a language model to reason (about how to answer based on provided context, what actions to take, etc.)
What is LangGraph ?
LangGraph is a library that extends LangChain, providing cyclic computational capabilities for LLM applications. While LangChain supports defining computation chains (Directed Acyclic Graphs or DAGs), LangGraph enables the incorporation of cycles. This allows for more intricate, agent-like behaviors, where an LLM can be called in a loop to determine the next action to take.

**Key Concepts**
Stateful Graph: LangGraph revolves around the concept of a stateful graph, where each node in the graph represents a step in our computation, and the graph maintains a state that is passed around and updated as the computation progresses.
Nodes: Nodes are the building blocks of your LangGraph. Each node represents a function or a computation step. We define nodes to perform specific tasks, such as processing input, making decisions, or interacting with external APIs.
Edges: Edges connect the nodes in your graph, defining the flow of computation. LangGraph supports conditional edges, allowing you to dynamically determine the next node to execute based on the current state of the graph.

**Steps involved in creating a graph using LangGraph:**
Define the Graph State : This represents the state of the graph.
Create the Graph.
Define the Nodes: Here we define the different functions associated with each workflow state.
Add nodes to the Graph: Here add our nodes to the graph and define the flow using edges and conditional edges.
Set Entry and End Points of the Graph.

**What is Tavily Search API ?**
Tavily Search API is a search engine optimized for LLMs, aimed at efficient, quick and persistent search results. Unlike other search APIs such as Serp or Google, Tavily focuses on optimizing search for AI developers and autonomous AI agents.

**What is Groq?**
Groq offers high-performance AI models & API access for developers with faster inference and at lower cost than competitors.
**
What is FastEmbed ?**
FastEmbed is a lightweight, fast, Python library built for embedding generation.

**Workflow of the RAG Agent**
Based on the question the Router decides whether to direct the question to retrieve context from vectorstore or perform a web search.
If the Router decides the question ha to be directed for retrieval from vectorstore, then matching documents are retrieved from the vectorstore otherwise perform a web search using tavily-api search
The document grader then grades the documents as relevant or irrelevant.
If the context retrieved is graded as relevant then check for hallucination using the hallucination grader. If the grader decides the response to be devoid of hallucination then present the response top the user.
In case the context is graded as irrelevant then perform a web search to retrieve the content.
Post retrieval , the document grader grades the content generated from web search .If found relevant the response is synthesized by using LLM and then presented

**Technology Stack Used**
Embedding Model : BAAI/bge-base-en-v1.5
LLM : Llam-3–8B
Vectorstore : Chroma
Graph /Agent : LangGraph

Please find code implementation in attached python file in this repository.
