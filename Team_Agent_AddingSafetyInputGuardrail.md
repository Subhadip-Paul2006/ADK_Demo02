# 🤖 Team Agent Documentation – Part 04

## 🛡️ Adding Safety: Input Guardrail using `before_model_callback`

---

## 🚀 Introduction

Ab tak tumhara system:

* ✔ Multi-agent hai
* ✔ Memory use karta hai
* ✔ Personalization karta hai

👉 Lekin ek **real-world problem** abhi bhi hai:

❌ User kuch bhi input de sakta hai
❌ Harmful / irrelevant / unwanted queries aa sakti hain
❌ LLM blindly process kar deta hai

---

## 🔥 Problem Statement

👉 Tumhara agent currently:

* Har input ko accept karta hai
* LLM ko bhej deta hai
* Without checking

---

### ⚠️ Danger:

* Abuse / unsafe content
* Irrelevant queries
* Cost waste (LLM calls expensive hote hain)

---

## 🛡️ Solution: Guardrails

👉 Guardrails = Safety filters

---

## 🧠 What is `before_model_callback`?

Ye ek **hook function** hai jo:

👉 LLM call hone se *just pehle* execute hota hai

---

### 💡 Simple Samajh:

```
User Input → (Callback Check) → LLM → Response
```

---

### 🔥 MOST IMPORTANT LINE:

👉 Ye LLM ko call hone se **pehle intercept karta hai**

---

## 🧠 Why This is Powerful?

Kyuki:

👉 Tum control karte ho:

* Kya LLM tak jaana chahiye
* Kya block hona chahiye

---

## ⚙️ Where It Fits in Flow

Normal flow:

```
User → Runner → Agent → LLM → Response
```

With guardrail:

```
User → Runner → Agent → 🔍 Callback → LLM → Response
```

---

## 🧠 Callback kya karta hai?

Callback 3 kaam kar sakta hai:

---

### 1. Inspect (Check)

👉 User message analyse karta hai

---

### 2. Modify

👉 Input ko change kar sakta hai

---

### 3. Block ❗ (MOST IMPORTANT)

👉 LLM call completely stop kar sakta hai

---

## 🔥 Core Concept (Golden Line)

👉 **If callback returns response → LLM call skip ho jata hai**

---

## ⚙️ Step 1: Guardrail Function Banana

Is step mein humne ek function banaya jo:

👉 User ke message ko check karega

---

### 🧠 Logic:

* User input read karo
* Check karo kya "BLOCK" word hai
* Agar hai → request reject karo

---

## 🔍 Message Extraction

Callback ko milta hai:

👉 Full LLM request (history + current message)

---

### Important Step:

👉 Last user message identify karna

---

## 🔁 Guardrail Logic

---

### Case 1: Keyword found ("BLOCK")

👉 System:

* LLM call cancel karega
* Direct response return karega
* State update karega (optional)

---

### Case 2: Keyword not found

👉 System:

* Normal flow continue karega
* LLM call hoga

---

## 🧠 State Interaction (Hidden Power)

Callback bhi state access kar sakta hai:

👉 Example:

* Flag store karna (blocked request detect hua)

---

## 🤖 Step 2: Root Agent Update

Ab humne apne root agent ko upgrade kiya:

---

### 🔥 New Feature Added:

👉 before_model_callback attach kiya

---

### 🧠 Meaning:

👉 Har request pe:

* Pehle callback run hoga
* Fir decision hoga

---

## ⚠️ Important Note

👉 Callback sirf **us agent pe apply hota hai jisme define hai**

---

### 💥 VERY IMPORTANT:

👉 Sub-agents automatically inherit nahi karte

---

## 🧠 System Behavior Now

Agent ka flow ab:

1. User input aaya
2. Callback run hua
3. Check hua
4. Decision:

   * Block
   * Allow

---

## ⚙️ Step 3: Testing the Guardrail

System ko 3 scenarios se test kiya gaya:

---

## 🔹 Case 1: Normal Input

👉 Example:
Weather query

---

### Flow:

* Callback run
* Keyword nahi mila
* LLM call allowed
* Normal response

---

## 🔹 Case 2: Blocked Input

👉 Example:
Message contains "BLOCK"

---

### Flow:

* Callback run
* Keyword detect hua
* LLM call cancel
* Direct response return

---

### 🧠 Key Insight:

👉 LLM ko call hi nahi kiya gaya

---

## 🔹 Case 3: Delegation Case

👉 Example:
Greeting

---

### Flow:

* Callback run (root agent pe)
* Allowed
* Root agent → greeting agent delegate
* Greeting agent execute

---

## ⚠️ CRITICAL UNDERSTANDING

👉 Callback sirf root agent pe run hua

👉 Greeting agent pe automatically apply nahi hua

---

## 🧠 Deep Understanding (Very Important)

Callback ke paas access hota hai:

* Agent name
* Session state
* Full request

---

### Iska matlab:

👉 Tum advanced logic likh sakte ho:

* Role-based filtering
* State-based control
* Dynamic rules

---

## 🧠 Real Mental Model

Socho:

👉 Callback = Security Guard
👉 LLM = VIP Room

---

### Flow:

* Guard check karta hai
* Decide karta hai:

  * Entry allow
  * Entry block

---

## 🏗️ Architecture / User Flow

```id="flow4"
              👤 User
                 ↓
          💬 Query Input
                 ↓
         ⚙️ Runner Engine
                 ↓
        🧠 Root Agent
                 ↓
        🛡️ Callback (Security Check)
                 ↓
        ┌────────┴────────┐
        ↓                 ↓
   ❌ Block          ✅ Allow
        ↓                 ↓
   Direct Response     🤖 LLM Call
        ↓                 ↓
        └────────┬────────┘
                 ↓
        🧠 Agent Decision
                 ↓
     🔁 (Optional Delegation)
                 ↓
           💬 Final Output
```

---

## 🔥 Final Summary (Quick Revision)

* before_model_callback = Pre-LLM hook
* Purpose = Safety + Control
* Can:

  * Inspect
  * Modify
  * Block

---

### 💥 Golden Rule:

👉 Return response → LLM skip
👉 Return None → LLM continue

---

## 💡 Real-World Use Cases

* Toxic input filtering
* API abuse prevention
* Cost control
* Prompt injection defense
* Policy enforcement

---

## 🚀 Final Insight

👉 Ab tumne system mein:

* Intelligence ✔
* Memory ✔
* Safety ✔

add kar diya hai

---

## 🔮 What’s Next?

Next step:

👉 Tool-level guardrails
👉 Even deeper control system

---

## 🧠 Bro-Level Explanation (Final)

Agar simple line mein samajhna ho:

👉 Ye ek **filter hai jo decide karta hai ki LLM ko kaam karne dena hai ya nahi**

---
