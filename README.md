# Neo4j Knowledge Graph Guide

This document is part of a series of sections aimed at helping you set up, configure, and utilize Neo4j for knowledge graph creation and management. It starts with the basics and progressively delves into advanced topics.

---

# **Table of Contents**

## **Setting Up Neo4j for Knowledge Graph Creation**
1. [Sign Up for Neo4j](#1-sign-up-for-neo4j)
2. [Choose the Free Tier](#2-choose-the-free-tier)
3. [Download the Configuration File](#3-download-the-configuration-file)
4. [Open Neo4j Workspace](#4-open-neo4j-workspace)
5. [Create Your Knowledge Graph](#5-create-your-knowledge-graph)
6. [Useful Links](#6-useful-links)

## **Building a Question Answering Application**
7. [Overview](#7-overview)
8. [Notebook Workflow](#8-notebook-workflow)
9. [Key Components](#9-key-components)
10. [Example Code Snippets](#10-example-code-snippets)

---

# **Section 1: Setting Up Neo4j for Knowledge Graph Creation**

This guide provides step-by-step instructions for setting up Neo4j to create a knowledge graph. It includes details on signing up, downloading configuration files, and accessing the Neo4j workspace.

---

# **Neo4j Setup and Knowledge Graph Creation**

## **1. Sign Up for Neo4j**
1. Visit the Neo4j website: [https://neo4j.com](https://neo4j.com)
2. Click on **Get Started Free** or **Sign Up**.
3. Register with your email address or use your Google/GitHub account for quick registration.

---

## **2. Choose the Free Tier**
1. After signing up, navigate to the **AuraDB Free** tier, which offers a free cloud-hosted Neo4j instance.
2. Select **Create a Database**.
3. Provide a database name and password.
4. Click **Create** and wait for the database to initialize.

---

## **3. Download the Configuration File**
1. Once the database is created, download the configuration file (.txt) provided.
2. The file contains connection details, including:
   - Database URI
   - Username
   - Password
3. Store this file securely for later use.

---

## **4. Open Neo4j Workspace**
1. Go to the [Neo4j Workspace](https://neo4j.com/workspace).
2. Select **Connect to a Database**.
3. Use the URI, username, and password from the configuration file to log in.
4. Click **Connect**.

---

## **5. Create Your Knowledge Graph**
### Example Cypher Queries:
1. **Create Nodes**
```cypher
CREATE (p:Person {name: 'Alice', age: 30});
CREATE (p:Person {name: 'Bob', age: 25});
```
2. **Create Relationships**
```cypher
MATCH (a:Person {name: 'Alice'}), (b:Person {name: 'Bob'})
CREATE (a)-[:FRIEND]->(b);
```
3. **Query the Graph**
```cypher
MATCH (p:Person)-[:FRIEND]->(f:Person)
RETURN p.name, f.name;
```

---

## **6. Useful Links**
- **Neo4j Official Site**: [https://neo4j.com](https://neo4j.com)
- **Neo4j AuraDB Free Tier**: [https://neo4j.com/cloud/aura](https://neo4j.com/cloud/aura)
- **Neo4j Workspace**: [https://neo4j.com/workspace](https://neo4j.com/workspace)
- **Cypher Query Language Docs**: [https://neo4j.com/docs/cypher-manual](https://neo4j.com/docs/cypher-manual)

---

# **Section 2: Building a Question Answering Application**

## **7. Overview**
This section explains how to build a Question Answering (QA) application over a Graph Database using Neo4j. The provided notebook demonstrates querying and retrieving answers directly from the graph database.

---

## **8. Notebook Workflow**
The workflow in the provided Jupyter Notebook focuses on:
1. Setting up database connections.
2. Creating and populating the graph database from a CSV file.
3. Implementing a **GraphCypherQAChain** to process natural language questions.
4. Generating Cypher queries based on the input questions.
5. Executing the Cypher queries and retrieving results from the database.
6. Displaying results in an interpretable format.

---

## **9. Key Components**
- **Database Connection**: Establishes communication with the Neo4j instance.
- **CSV Import**: Loads data from a CSV file to create nodes and relationships in the graph database.
- **Cypher Query Generation**: Uses a **GraphCypherQAChain** to dynamically generate queries based on user input.
- **Query Execution**: Sends Cypher queries to the database and retrieves answers.
- **LLM Integration**: Uses a Language Model (LLM) to interpret questions and generate queries.
- **Result Parsing**: Extracts and formats results for QA outputs.
- **Visualization**: Displays graphs and connections visually.

---

## **10. Example Code Snippets**
1. **Connecting to Neo4j**
```python
from neo4j import GraphDatabase
URI = "neo4j+s://<your-database-uri>"
NEO4J_USERNAME="neo4j"
NEO4J_PASSWORD="rQJMGc6ongtdUh6iWZ27jOg5QeyqBcMq3JWxUJ3_Y"
```
2. **Loading CSV Data into Neo4j**
```cypher
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row
CREATE (p:Person {name: row.name, age: toInteger(row.age)});
```
3. **GraphCypherQAChain Implementation**
```python
from langchain.chains import GraphCypherQAChain
chain = GraphCypherQAChain.from_llm(graph, llm, verbose=True)
result = chain.run("Who are Alice's friends?")
print(result)
```
---

With this section, you can create a knowledge graph from CSV data and build QA systems using Neo4j and LLMs!

