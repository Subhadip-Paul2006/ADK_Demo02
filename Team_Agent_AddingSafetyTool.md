# 🤖 Team Agent Documentation – Part 05

## 🛡️ Adding Safety: Tool Argument Guardrail (`before_tool_callback`)

---

## 🚀 Introduction

Ab tak tumne system mein:

* ✔ Multi-agent delegation
* ✔ Memory (Session State)
* ✔ Input safety (`before_model_callback`)

add kar diya hai

---

👉 Lekin ek **hidden danger** abhi bhi exist karta hai:

❌ LLM galat tool arguments generate kar sakta hai
❌ Unsafe ya restricted tool calls ho sakte hain
❌ Tools misuse ho sakte hain

---

## 🔥 Problem Statement

Step 5 tak:

👉 Tumne user input filter kar liya

BUT…

👉 LLM ke decision ko abhi tak blindly trust kar rahe ho

---

### ⚠️ Danger Example:

User: “Weather in Paris”

👉 LLM:

* Tool call karega → city = Paris

👉 But suppose:

* Paris restricted hai
* Costly API hai
* Policy violation hai

---

## 🛡️ Solution: Tool-Level Guardrail

👉 Is problem ko solve karta hai:

🔥 **before_tool_callback**

---

## 🧠 What is `before_tool_callback`?

Ye ek function hai jo:

👉 Tool execute hone se *just pehle* run hota hai

---

### 💡 Simple Flow:

```id="flowt1"
User → LLM → Tool Call → 🔍 Callback → Tool Execute
```

---

### 🔥 Golden Line:

👉 **LLM ne tool decide kar liya hai, but tool run hone se pehle tum control lete ho**

---

## 🧠 Why This is Important?

Kyuki:

👉 LLM hamesha correct nahi hota
👉 Wo galat ya unsafe arguments generate kar sakta hai

---

### 🔥 So:

👉 before_model_callback = Input control
👉 before_tool_callback = Execution control

---

## ⚙️ Where It Fits in System

Full flow now:

```id="flowt2"
User Input
   ↓
🛡️ before_model_callback
   ↓
🤖 LLM Decision
   ↓
🛠️ Tool Selected
   ↓
🛡️ before_tool_callback
   ↓
🛠️ Tool Execution
   ↓
Response
```

---

## 🧠 Callback kya check karta hai?

Callback ke paas 3 cheeze hoti hain:

---

### 1. Tool

👉 Kaunsa tool call ho raha hai

---

### 2. Arguments

👉 LLM ne kya parameters pass kiye

---

### 3. ToolContext

👉 Session state + agent info

---

## 🔥 Core Power

Callback:

* Tool arguments inspect karta hai
* Modify kar sakta hai
* Block kar sakta hai

---

## ⚙️ Step 1: Guardrail Logic Design

Is step mein humne ek rule banaya:

👉 “Paris ke liye weather allow nahi hai”

---

### 🧠 Logic:

* Check karo:

  * Tool = weather tool
  * City = Paris

---

### 🔁 Decision:

---

### ❌ Case 1: Paris detected

👉 Tool execution block

---

### ✅ Case 2: Other city

👉 Tool allow

---

## 🛑 Blocking Mechanism

👉 Yahan sabse important concept hai:

---

### 💥 Golden Rule:

👉 **If callback returns dictionary → tool run nahi hota**

---

### 🧠 Instead kya hota hai?

👉 Wo dictionary hi tool ka output ban jata hai

---

## 🔁 Normal Flow vs Blocked Flow

---

### ✅ Normal Flow

* Callback → allow
* Tool run
* Real output

---

### ❌ Blocked Flow

* Callback → block
* Tool skip
* Fake (controlled) response return

---

## 🧠 Mental Model

Socho:

👉 Tool = Machine
👉 Callback = Safety Switch

---

### Flow:

* Machine start hone se pehle
* Safety system check karta hai

---

## 🤖 Step 2: Root Agent Update

Ab humne root agent ko upgrade kiya:

---

### 🔥 New Features:

* before_model_callback (input guardrail)
* before_tool_callback (tool guardrail)

---

### 🧠 Meaning:

👉 Double protection system

---

## 🧠 Combined Safety Layers

System ab 2 layers pe protect karta hai:

---

### Layer 1: Input Guardrail

👉 User message check

---

### Layer 2: Tool Guardrail

👉 Tool arguments check

---

## ⚙️ Step 3: Testing the Tool Guardrail

System ko 3 scenarios se test kiya gaya:

---

## 🔹 Case 1: Allowed City (New York)

---

### Flow:

* Input safe
* LLM tool call karta hai
* Callback args check karta hai
* Allowed
* Tool execute

---

## 🔹 Case 2: Blocked City (Paris)

---

### Flow:

* Input safe
* LLM tool call karta hai
* Callback detect karta hai "Paris"
* Tool block

---

### 🧠 Important:

👉 Tool run hi nahi hota

---

### Output:

👉 Custom error message

---

## 🔹 Case 3: Another Allowed City (London)

---

### Flow:

* Same as normal
* Tool successfully run

---

## ⚠️ Critical Understanding

👉 Callback tool ke naam pe bhi depend karta hai

👉 Sirf specific tool ko block kiya gaya hai

---

## 🧠 State Interaction

Callback state update bhi kar sakta hai:

👉 Example:

* guardrail_tool_block_triggered = True

---

### 💡 Why useful?

* Logging
* Monitoring
* Analytics

---

## 🧠 Deep Understanding

Ab system 4 layers pe kaam kar raha hai:

---

### 🔥 1. Agent Logic

Decision making

---

### 🔥 2. Tool Logic

Execution

---

### 🔥 3. State Memory

Context

---

### 🔥 4. Safety Guardrails

Control

---

## 🏗️ Architecture / User Flow

```id="flow5"
                👤 User
                   ↓
            💬 Query Input
                   ↓
        🛡️ Input Guardrail
                   ↓
            🤖 LLM Decision
                   ↓
           🛠️ Tool Selected
                   ↓
        🛡️ Tool Guardrail
                   ↓
        ┌────────┴────────┐
        ↓                 ↓
   ❌ Block          ✅ Allow
        ↓                 ↓
   Custom Output      Tool Execution
        ↓                 ↓
        └────────┬────────┘
                 ↓
            🧠 Agent Response
                 ↓
            💬 Final Output
```

---

## 🔥 Final Summary (Quick Revision)

* before_tool_callback = Tool safety layer
* Checks:

  * Tool name
  * Arguments
* Can:

  * Modify
  * Block
  * Allow

---

### 💥 Golden Rules:

👉 Return dict → Tool skip
👉 Return None → Tool run

---

## 💡 Real-World Use Cases

* API cost control
* Restricted data access
* Fraud prevention
* Input sanitization
* Compliance rules

---

## 🚀 Final Insight

👉 Ab tumhara system:

❌ Basic AI nahi hai
✅ Fully controlled, safe AI system hai

---

## 🧠 Bro-Level Explanation

Agar ek line mein samajhna ho:

👉 “LLM ne jo decide kiya, usko blindly execute nahi karte — pehle verify karte hain”

---

## 🔮 What’s Next?

Ab tum ready ho:

* Production-level agents
* Hackathon-winning projects
* Real-world AI systems

---
