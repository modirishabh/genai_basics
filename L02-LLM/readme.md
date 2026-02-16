```markdown
# Understanding How LLMs (Like ChatGPT / Gemini) Actually Work

This document explains how Large Language Models (LLMs) function — especially around topics like calculation, prediction, external tools, context handling, and API usage.

---

# 1️⃣ Does an LLM Really Calculate 2 + 2?

When you ask:

```

2 + 2 = ?

```

The model answers `4`.

### But what actually happens?

LLMs:
- Break text into **tokens**
- Predict the **next most probable token**
- Use patterns learned during training

The model has seen `"2 + 2 = 4"` thousands of times during training.  
So it predicts `4` based on probability — not by doing symbolic arithmetic like a calculator.

### Important:

LLMs are **pattern predictors**, not symbolic math engines.

---

# 2️⃣ Can LLMs Perform Calculations?

There are two situations:

## 🧠 A) Pure LLM (No External Tools)

- Uses learned patterns
- Does not execute arithmetic step-by-step
- May fail on large numbers

Example:

```

123456789 × 987654321

```

A pure LLM may give incorrect results.

---

## 🛠️ B) LLM + External Tools

Modern systems (ChatGPT, Gemini, etc.) can:

- Generate Python code
- Execute it via tool integration
- Perform web searches
- Access real-time data

Flow:

1. LLM writes code
2. Tool executes code
3. Result returns to LLM
4. LLM formats result into natural language

This is called:

- Tool Augmentation
- Function Calling
- Agent-based systems

---

# 3️⃣ Why Does It Sometimes Count Letters Wrong?

Example:

```

How many R’s are in "strawberry"?

```

Correct answer: **3**

A pure LLM may say **2** because it predicts from patterns instead of counting characters.

Modern models sometimes use internal reasoning or tool assistance to improve accuracy.

---

# 4️⃣ Why Can't LLMs Give Real-Time Data?

LLMs:

- Are trained on static datasets
- Do not have live internet access by default
- Do not update continuously

So they cannot know:
- Today's temperature
- Current date
- Live stock prices

Unless connected to:
- Web APIs
- Databases
- External tools

---

# 5️⃣ What is Context?

Context is **previous conversation history** sent to the model.

In ChatGPT UI:

Each request includes:

```

System Prompt

* Previous Messages
* Current Message

```

Example:

```

User: Hi I am Mohit
User: What is my name?

```

Works because previous message is included in context.

---

### But in API calls:

If you send only:

```

"What is my name?"

```

The model will respond:

```

I don't know your name.

````

Because no context was provided.

---

# 6️⃣ API Interaction Explained

Two approaches were shown:

---

## 🧩 Method 1: Manual History Management

You maintain conversation history manually:

```js
let history = []
````

For each message:

* Push user message
* Push model response
* Send entire history every time

---

## 🧩 Method 2: Built-in Chat Object

```js
ai.chat.create()
```

This automatically:

* Maintains history
* Handles conversation flow
* Simplifies interaction

This is cleaner and recommended.

---

# 7️⃣ Why Is `await` Important?

API calls are asynchronous.

Without `await`:

* Code continues executing
* Response may not arrive before next step runs

Correct usage:

```js
await chat.sendMessage()
```

This pauses execution until the response is received.

---

# 8️⃣ Key Technical Truths

| Concept                              | Reality |
| ------------------------------------ | ------- |
| LLM calculates like a calculator     | ❌ No    |
| LLM predicts next token              | ✅ Yes   |
| LLM knows real-time data             | ❌ No    |
| With tools, it can access live data  | ✅ Yes   |
| Context is necessary                 | ✅ Yes   |
| API requires manual context handling | ✅ Yes   |

---

# 9️⃣ Are LLMs Just Pattern Repeaters?

Not exactly.

Modern LLMs:

* Learn deep internal representations
* Simulate reasoning
* Can approximate arithmetic internally
* Use attention mechanisms

They are not symbolic engines — but they are more than simple parrots.

---

# 🔟 Final Summary

An LLM is:

* Not a brain
* Not a calculator
* Not a live database

It is:

> A probability engine trained on language patterns.

When combined with tools, it becomes extremely powerful.

---

# 🚀 What You Can Learn Next

If you want to go deeper:

* How Transformers work
* What Tokenization is
* How Attention Mechanism works
* How Tool Calling works internally
* How to build your own AI agent

---

**End of README**

```
```
