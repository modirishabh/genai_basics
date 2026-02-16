```markdown
# 🚀 Mini Cursor AI (Website Builder using LLM + Terminal Commands)

This project demonstrates how to build a **mini version of Cursor AI** using:

- 🧠 LLM (Large Language Model)
- 🛠 Custom Tool (Command Executor)
- 💻 Node.js
- ⚙️ Terminal / Shell Commands

The core idea is simple:

> LLM generates commands → Tool executes them → Website gets built automatically.

---

# 📌 Core Concept

## ❓ Problem

LLMs can:
- Generate text
- Generate code
- Suggest terminal commands

But they **cannot:**
- Create folders directly
- Create files
- Execute system commands

So how do we build websites automatically?

---

## 💡 Solution

We create a **custom tool** that:

- Accepts a terminal command (string)
- Executes it using Node.js
- Returns output or error

Architecture:

```

User → LLM → executeCommand Tool → Operating System

```

---

# 🏗 System Architecture

### Step-by-Step Flow

1. User says:  
```

Create a calculator website

```

2. LLM analyzes and responds with:
```

mkdir calculator

```

3. Tool executes the command.

4. LLM gives next command:
```

touch calculator/index.html

````

5. Tool executes it.

6. LLM writes HTML, CSS, JS using terminal commands.

7. Website is fully built.

---

# 🔧 Technical Implementation

## 1️⃣ Install Dependencies

```bash
npm init -y
npm install child_process util readline-sync @google/generative-ai
````

---

## 2️⃣ Command Execution Tool

We use Node.js `child_process` to execute terminal commands.

```js
import { exec } from "child_process";
import util from "util";

const execPromise = util.promisify(exec);

async function executeCommand(command) {
  try {
    const { stdout, stderr } = await execPromise(command);

    if (stderr) {
      return { status: "error", message: stderr };
    }

    return { status: "success", message: stdout };
  } catch (error) {
    return { status: "error", message: error.message };
  }
}
```

This function:

* Runs shell command
* Waits for completion
* Returns output or error

---

# 🧠 AI Agent Concept

AI Agent = LLM + Tools

LLM:

* Thinks
* Plans steps
* Generates commands

Tool:

* Executes commands
* Modifies system files

---

# 📋 System Instructions (Very Important)

We guide the LLM using system prompts:

Example:

```
You are a website builder expert.
Analyze user query.
Give step-by-step terminal commands.
Use available tool: executeCommand.
Create folder → create files → write code.
Provide OS compatible commands.
```

Prompt engineering is the main power here.

---

# 🖥 OS Handling (Mac vs Windows)

Different OS have different command formats.

We detect OS:

```js
import os from "os";

const platform = os.platform();
```

Then instruct LLM:

> Provide commands according to current operating system.

---

# ⚠ Important: Avoid echo for Multi-line Code

❌ Risky:

```bash
echo "multi line code" > file.js
```

It may break due to quotes.

✅ Better (Mac/Linux):

```bash
cat <<EOF > file.js
multi line code here
EOF
```

Windows PowerShell requires a different format.

---

# 🎯 Example Output

## Input:

```
Create a coding course selling website
```

## System Automatically:

* Creates folder
* Creates index.html
* Creates style.css
* Creates script.js
* Writes full frontend code

Then you run Live Server and it works.

---

# 🤯 What You Built

You created a **Mini Cursor AI** that:

* Understands natural language
* Converts it to terminal commands
* Builds real projects
* Works step-by-step

---

# 🧩 Why Pre-Building Templates Is Wrong

Old approach:

* Pre-create calculator code
* Pre-create weather app
* Pre-create blog template

Problems:

* Not scalable
* Manual effort
* Limited flexibility

New approach:

* Dynamic generation
* Infinite possibilities
* Fully automated

---

# 🔥 Key Learnings

* LLM cannot execute code
* Tools give execution ability
* Promises ensure step-by-step execution
* Prompt engineering is critical
* AI Agents = LLM + Tools + Instructions

---

# 🧠 Mental Model

```
User = Boss
LLM = Brain
Tool = Hands
```

Boss gives order
Brain plans
Hands execute

---

# 📌 Future Improvements

* Run this inside browser
* Show live command output
* Show AI thinking steps
* Add project preview panel
* Add code editor view
* Build full web-based AI builder

---

# 🏁 Conclusion

This project demonstrates:

> The real power of AI is unlocked when you combine LLM + Execution Tools.

You are no longer just generating text.

You are building systems.

---

# 📜 License

Open for learning and experimentation.

---

**Built with Node.js + LLM + AI Agent Architecture**

```
```
यह पूरा लेक्चर असल में एक बहुत ही powerful concept समझा रहा है:

> **LLM खुद कोड run नहीं कर सकता, लेकिन वह आपको command दे सकता है — और आप (या आपका tool) उन commands को run करके कुछ भी बनवा सकते हो।**

मैं इसे आपके लिए simple भाषा में step-by-step समझा देता हूँ 👇

---

# 🔥 Core Idea क्या है?

## 1️⃣ LLM क्या कर सकता है?

* टेक्स्ट लिख सकता है
* कोड लिख सकता है
* टर्मिनल कमांड लिख सकता है
* गाइड कर सकता है

❌ लेकिन

* VS Code में file create नहीं कर सकता
* Folder नहीं बना सकता
* Code run नहीं कर सकता

---

## 2️⃣ Problem क्या है?

अगर user बोले:

> “मुझे calculator वेबसाइट बना दो”

LLM क्या करेगा?

* HTML लिख देगा
* CSS लिख देगा
* JS लिख देगा

लेकिन:

* index.html कौन बनाएगा?
* folder कौन बनाएगा?
* file में code कौन डालेगा?

👉 ये काम सिस्टम को करना पड़ेगा।

---

# 🧠 Smart Solution क्या है?

हम एक **Tool** बना देते हैं।

एक ऐसा function जो:

```
executeCommand("mkdir calculator")
```

जैसी command को सच में run कर दे।

---

# 🏗 पूरा सिस्टम कैसे काम करता है?

## Architecture

```
User → LLM → Tool (executeCommand) → System
```

### Step-by-step:

1. User: “Calculator बना दो”
2. LLM सोचता है:

   * पहले folder बनाना होगा
   * फिर HTML file
   * फिर CSS
   * फिर JS
3. LLM command देता है:

   ```
   mkdir calculator
   ```
4. आपका tool इसे run कर देता है
5. फिर LLM अगली command देता है:

   ```
   touch calculator/index.html
   ```
6. Tool run करता है
7. फिर LLM HTML का content लिखने के लिए command देता है
8. Tool फिर run करता है

💥 Result: पूरी वेबसाइट auto बन जाती है

---

# 💡 पहले वाला approach क्यों गलत था?

वीडियो में पहले एक approach बताया गया था:

> हर वेबसाइट का code पहले से बना कर रख दो (calculator, weather app, etc.)

Problem:

* हर चीज manually बनानी पड़ेगी
* Unlimited websites नहीं बना सकते
* Scale नहीं होगा

इसलिए वो approach reject कर दी गई।

---

# 🚀 Real Magic कहाँ है?

Magic यहाँ है:

> LLM सिर्फ instructions देता है
> Tool उन instructions को execute करता है

आपने LLM को:

* एक tool दे दिया
* OS बता दिया (Mac / Windows)
* Proper system instructions दे दिए

बस game over 🔥

---

# ⚙️ Technical Core चीजें

## 1️⃣ child_process क्या है?

Node.js में:

```js
import { exec } from "child_process"
```

इससे आप system commands run कर सकते हो।

---

## 2️⃣ util.promisify क्यों use किया?

क्योंकि:

* commands step-by-step चलनी चाहिए
* पहले folder बने
* फिर file बने
* फिर content डले

अगर async properly handle नहीं किया तो error आएगा।

---

## 3️⃣ System Prompt क्यों important है?

आपने LLM को बताया:

* तुम website builder expert हो
* step-by-step command देना
* OS के हिसाब से command देना
* single terminal command देना

💡 LLM को clear instructions दोगे तो output perfect मिलेगा।

---

# 🖥 OS वाला Important Point

Mac और Windows की commands अलग हो सकती हैं।

Example:

Mac:

```
cat <<EOF > file.js
code here
EOF
```

Windows PowerShell:
Different syntax

अगर ये नहीं बताया तो code टूट सकता है।

---

# 🧨 echo Command Dangerous क्यों?

```
echo "multi line code" > file.js
```

Problem:

* multi-line content में टूट सकता है
* quotes गलत पकड़ सकता है

Better:

```
cat <<EOF > file.js
multi line code
EOF
```

---

# 🤯 Actually ये क्या बना रहे हैं?

आप basically बना रहे हो:

> Mini Cursor AI

Cursor क्या करता है?

* Prompt लो
* Code generate करो
* Files बनाओ
* Project build करो

आपने वही basic version बना लिया।

---

# 💎 Final समझ

ये project सिखाता है:

1. AI agent = LLM + Tools
2. LLM सोचता है
3. Tool काम करता है
4. User सिर्फ बोलता है
5. System auto build करता है

---

# 🧠 इसे और simple में समझो

LLM = Brain
Tool = Hands
User = Boss

Boss बोलता है
Brain सोचता है
Hands काम करते हैं

---

अगर आप चाहो तो मैं:

* इसका पूरा flow diagram बना दूँ
* या simplified version code explain कर दूँ
* या browser version कैसे बनाना है वो समझा दूँ

बस बताओ 😊
