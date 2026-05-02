# 🤖 Team Agent Documentation – Part 03

## 🧠 Adding Memory & Personalization with Session State

---

## 🚀 Introduction

Ab tak humne kya banaya?

* Step 1 → Single Agent
* Step 2 → Agent Team (Delegation)

👉 Lekin ek problem hai:

❌ Har baar agent fresh start karta hai
❌ User ki previous baatein ya preferences yaad nahi rehti

---

## 🔥 Solution: Memory System (Session State)

Ab hum introduce karte hain:

👉 **Session State (Memory System)**

---

## 🧠 What is Session State?

Session State ek **dictionary (key-value storage)** hota hai jo:

* Ek specific user session se linked hota hai
* Multiple conversation turns ke beech data store karta hai
* Agents aur tools dono access kar sakte hain

---

### 💡 Simple Samajh:

👉 Session State = “Agent ka memory box”

---

## 🧠 Why Memory is Important?

Without memory:

* Har query isolated hoti hai
* Personalization impossible hota hai

With memory:

* Agent user preferences yaad rakhta hai
* Context-aware responses deta hai
* Smart behavior possible hota hai

---

## ⚙️ Step 1: New Session + Initial State

Is step mein hum:

👉 Ek **naya session service** create karte hain
👉 Ek **initial state define karte hain**

---

### 🧾 Example Concept:

User preference store kiya:

* Temperature unit = Celsius

---

### 🧠 Important:

👉 State session ke saath attach hota hai
👉 Alag user → alag memory

---

## 🔍 State Verification

Session create karne ke baad:
👉 Hum check karte hain ki state correctly store hua ya nahi

---

## 🛠️ Step 2: Stateful Tool Banana

Ab humne ek upgraded tool banaya:

👉 **State-aware weather tool**

---

## 🔥 Key Concept: ToolContext

👉 Ye sabse important concept hai is step ka

ToolContext allow karta hai:

* Tool ko session state read karne
* Tool ko state update karne

---

### 💡 Simple Samajh:

ToolContext = “Tool ka connection with memory”

---

## 🧠 Tool ka Smart Behavior

Tool ab ye karta hai:

1. State se user preference read karta hai
2. Uske basis pe output change karta hai

---

### 🧪 Example:

State:
👉 Celsius

Output:
👉 25°C

---

State change:
👉 Fahrenheit

Output:
👉 77°F

---

## 🔁 State Read + Write

Tool 2 kaam karta hai:

### 1. Read

👉 User preference read karta hai

### 2. Write

👉 Last city checked store karta hai

---

## ⚠️ Best Practice

State read karte time:

👉 Always default value use karo

Kyun?
👉 Crash avoid hota hai agar key missing ho

---

## 🤖 Step 3: Agent Upgrade (Stateful Root Agent)

Ab humne apne root agent ko upgrade kiya:

---

### 🔥 New Features:

* Stateful tool use karta hai
* Sub-agents (greeting/farewell) still active
* Memory-aware responses deta hai

---

## 💾 Key Feature: output_key

👉 Ye ek powerful shortcut hai

---

### 🧠 What it does:

👉 Agent ka final response automatically state mein save karta hai

---

### 💡 Example:

State mein save hoga:
👉 last_weather_report

---

## 🔁 Important Behavior

👉 Har new response old value overwrite karega

---

## ⚙️ Step 4: Testing Memory Flow

Ab humne system ko test kiya multiple steps mein:

---

### 🔹 Step 1: Weather Check (Initial State)

👉 Tool state read karta hai
👉 Celsius use karta hai

---

### 🔹 Step 2: Manual State Update

👉 Humne manually state change kiya

Celsius → Fahrenheit

---

### ⚠️ Important Concept:

👉 Session copy modify karne se change nahi hota
👉 Actual stored state change karna padta hai

---

## 🔹 Step 3: Weather Check Again

👉 Tool updated state read karta hai
👉 Output ab Fahrenheit mein aata hai

---

## 🔹 Step 4: Greeting Test

👉 Delegation still works

---

## 🔹 Step 5: Final State Check

👉 State inspect kiya gaya

---

### 🧾 Expected Values:

* Temperature unit → Fahrenheit
* Last weather report → latest response
* Last city checked → stored by tool

---

## 🧠 Key Learnings

### 🔥 1. State Persistence

Data multiple turns tak survive karta hai

---

### 🔥 2. Personalization

Agent user preference ke hisaab se behave karta hai

---

### 🔥 3. Tool Intelligence

Tool static nahi hai → dynamic ban gaya

---

### 🔥 4. output_key Automation

Manual saving ki need nahi

---

## 🏗️ Architecture / User Flow

```id="flow3"
              👤 User
                 ↓
          💬 Query Input
                 ↓
         ⚙️ Runner (Engine)
                 ↓
        🧠 Root Agent (Stateful)
                 ↓
        🔍 Read Session State
                 ↓
   ┌────────────┼────────────┐
   ↓            ↓            ↓
👋 Greeting   🌦️ Weather   👋 Farewell
 Agent         Agent         Agent
   ↓            ↓            ↓
             🛠️ Tool (Stateful)
                 ↓
        🔁 Read + Write State
                 ↓
        🧠 Generate Response
                 ↓
        💾 Save via output_key
                 ↓
           💬 Final Output
```

---

## 🔥 Final Summary (Quick Revision)

* Session State = Memory
* ToolContext = State access
* output_key = Auto-save
* Tool = Dynamic behavior
* Agent = Personalized response

---

## 💡 Pro Insight (Very Important)

Ab tumhara system:

❌ Static bot nahi raha
✅ Context-aware AI system ban gaya

---

### Real-world Use:

* User preferences (language, theme, etc.)
* Chat history memory
* Recommendation systems
* Personalized assistants

---

## 🚀 What’s Next?

Next level mein tum seekhoge:

👉 Safety guardrails
👉 Control system
👉 Production-level agent design

---
