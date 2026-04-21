# Neo4j TV Series Chatbot using Gradio

This repository contains a simple chatbot application that connects to a **Neo4j graph database** to answer questions about TV series.

The chatbot accepts natural language questions in **Indonesian**, converts them into **Cypher queries**, retrieves data from Neo4j, and displays the results using a **Gradio web interface**.

---

# 📌 Overview

This project demonstrates how to:

* Connect Python to a Neo4j database
* Extract keywords from natural language questions
* Generate Cypher queries dynamically
* Query graph-based TV series data
* Build a chatbot interface using Gradio

The system supports questions related to:

* Cast (pemain)
* Genre
* Director (sutradara)
* Citizenship (warga negara)
* Number of episodes

---

# ⚙️ Technologies Used

* Python
* Neo4j Graph Database
* Gradio
* Regular Expressions (re)

---

# 🧠 How It Works

The chatbot processes user questions through several steps:

## Step 1 — Extract Keywords

Keywords are detected from the input question:

Examples:

* siapa
* pemain
* genre
* sutradara
* episode

---

## Step 2 — Extract Title

Regular expressions are used to extract TV series titles.

Example pattern:

```python
pattern = r"(?i)siapa(?:kah)? pemain(?:\s+\w+)* (?:drama|series) (.+?)[\?\.]"
```

---

## Step 3 — Generate Cypher Query

The system generates Cypher queries dynamically.

Example:

```cypher
MATCH (s)-[:HAS_CAST]->(c)
WHERE s.name = 'Breaking Bad'
RETURN c.label AS cast
```

---

## Step 4 — Query Neo4j

The query is executed:

```python
with driver.session(database="tvseries") as session:
    result = session.run(query)
```

---

## Step 5 — Display Results

Results are displayed using:

```python
Gradio Chat Interface
```

Accessible at:

```bash
http://127.0.0.1:7860
```

---

# 💬 Supported Question Types

The chatbot supports the following Indonesian question formats:

---

## 🎭 Cast Query

**Example:**

```text
Siapa pemain drama Breaking Bad?
```

Returns:

```text
cast: Bryan Cranston
cast: Aaron Paul
...
```

---

## 🎬 Genre Query

**Example:**

```text
Series Breaking Bad memiliki genre apa?
```

Returns:

```text
genre: Crime
genre: Drama
```

---

## 🎥 Director Query

**Example:**

```text
Siapa sutradara series Breaking Bad?
```

Returns:

```text
director_name: Vince Gilligan
```

---

## 🌍 Citizenship Query

**Example:**

```text
Apa warga negara pemain series Breaking Bad?
```

Returns:

```text
cast: Bryan Cranston
warga_negara: United States
```

---

## 📺 Episode Count Query

**Example:**

```text
Series yang memiliki jumlah episode lebih dari 100
```

Returns:

```text
series: The Game
series: Saturday Night Live
series: ER
...
```

Supported operators:

* lebih dari ( > )
* kurang dari ( < )
* sama dengan ( = )

---

# 🖥️ Chatbot Interface

The chatbot interface is created using:

```python
gr.Interface(
    fn=chatbot,
    inputs=["text", "state"],
    outputs=["chatbot", "state"]
).launch(debug=True)
```

Local access:

```text
http://127.0.0.1:7860
```

To create a public link:

```python
launch(share=True)
```

---

# 📊 Example Graph Model

The Neo4j graph includes:

Nodes:

* Series
* Cast
* Genre
* Director
* Citizenship

Relationships:

* HAS_CAST
* HAS_GENRE
* HAS_DIRECTOR
* CITIZENSHIP

Example:

```cypher
(Series)-[:HAS_CAST]->(Cast)
(Cast)-[:CITIZENSHIP]->(Country)
```

---

# 📚 Learning Objectives

This project helps understand:

* Graph databases
* Cypher query language
* Natural language query parsing
* Neo4j-Python integration
* Chatbot development
* Graph-based recommendation systems

---

# 👩‍💻 Author

**Nabilah Hannania**

GitHub:
https://github.com/nabilahannania
