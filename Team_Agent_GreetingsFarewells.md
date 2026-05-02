# Team Agent Documentation – Part 02

## Building an Agent Team (Delegation for Greetings & Farewells)

---

## Introduction

Pehle wale step mein humne ek **single agent (weather agent)** banaya tha jo sirf ek kaam karta tha — weather batana.

Lekin real-world AI systems mein:
👉 Users sirf ek type ke questions nahi puchte
👉 Unke queries mixed hote hain (hello, bye, info, etc.)

Isliye yahan hum ek powerful concept introduce karte hain:

**Agent Team System**

---

## What is an Agent Team?

Agent Team ka matlab:

👉 Ek single agent ke instead multiple **specialized agents** banate hain
👉 Ek **main agent (root agent)** hota hai jo decide karta hai kaun kaam karega

---

### Structure:

* Root Agent → Manager / Coordinator
* Sub Agents → Specialists

---

## Why Agent Team? (Very Important)

Single agent approach problem:

* Instructions complex ho jaate hain
* Maintain karna mushkil hota hai
* Scalability low hoti hai

---

### Agent Team ke benefits:

### 1. Modularity

Har agent alag kaam karta hai → easy to manage

### 2. Specialization

Har agent apne kaam mein expert

### 3. Scalability

Naye features = naya agent add karo

### 4. Efficiency

Simple tasks ke liye lightweight agents use kar sakte ho

---

## Step 1: New Tools (Greeting & Farewell)

Ab humne 2 naye tools introduce kiye:

### Greeting Tool

* User ko hello bolne ke liye
* Name ho toh personalized greeting

### Farewell Tool

* Conversation end karne ke liye

---

### Important Understanding:

👉 Ye tools simple hain
👉 But inka use alag agents karenge

---

## Step 2: Sub-Agents Banana

Ab humne 2 naye agents banaye:

---

### Greeting Agent

👉 Kaam:

* Sirf greeting handle karega

👉 Behavior:

* Sirf hello bolna
* Aur kuch nahi karna

---

### Farewell Agent

👉 Kaam:

* Sirf goodbye bolna

👉 Behavior:

* Jab user bye bole → response de

---

## MOST IMPORTANT: Description Field

👉 Sub-agents ka **description** bahut critical hota hai

Kyun?

👉 Root agent isi ko read karke decide karta hai:
"Is query ko kisko bhejna hai?"

---

### Simple Samajh:

Description = Agent ka “resume”

---

## Step 3: Root Agent Upgrade (Weather Agent v2)

Ab humne apne main agent ko upgrade kiya:

👉 Ye ab sirf weather agent nahi hai
👉 Ye ek **team manager** ban gaya hai

---

### New Responsibilities:

* Weather handle kare
* Greeting detect kare
* Farewell detect kare
* Correct agent ko delegate kare

---

## Sub-Agent Linking

Root agent ko sub-agents diye gaye:

👉 Iska matlab:
"Ye agents tumhari team ka part hain"

---

## Core Concept: Automatic Delegation

Ye sabse powerful concept hai

👉 Jab user query aati hai:

1. Root agent usse analyse karta hai
2. Sub-agents ke description se match karta hai
3. Decide karta hai:

   * Khud handle kare
   * Ya kisi aur agent ko de

---

### Example:

User: "Hello bro"

👉 Root agent sochta hai:

* Ye weather nahi hai
* Ye greeting hai
* Greeting agent better hai

👉 Delegation hota hai

---

## Delegation Flow

👉 Step-by-step:

1. User query aayi
2. Root agent ne analyse kiya
3. Match mila (greeting/farewell)
4. Control transfer hua sub-agent ko
5. Sub-agent ne tool call kiya
6. Response generate hua
7. User ko output mila

---

## Decision Making Logic

Root agent 3 cheeze dekhta hai:

1. User query
2. Apni instructions
3. Sub-agents ke descriptions

👉 In sabka combination → decision

---

## Testing the Agent Team

System ko test karne ke liye 3 types ke queries use kiye:

---

### 1. Greeting Query

👉 Expected:
Greeting agent handle kare

---

### 2. Weather Query

👉 Expected:
Root agent khud handle kare

---

### 3. Farewell Query

👉 Expected:
Farewell agent handle kare

---

## Output Observation

Agar system sahi kaam kar raha hai:

* Greeting → greeting tool call
* Weather → weather tool call
* Farewell → goodbye tool call

👉 Isse confirm hota hai:
Delegation working
Agent team working

---

## Architecture / User Flow

```id="flow2"
           User
              ↓
        Query Input
              ↓
        Root Agent (Manager)
              ↓
    ┌─────────┼─────────┐
    ↓         ↓         ↓
Greeting  Weather  Farewell
 Agent        Agent        Agent
    ↓         ↓         ↓
  Tool      Tool      Tool
    ↓         ↓         ↓
    └─────────┼─────────┘
              ↓
        Response Merge
              ↓
        Final Output
```

---

## Final Summary (Quick Revision)

* Multiple agents = Agent Team
* Root agent = Decision maker
* Sub-agents = Specialists
* Description = Delegation key
* Delegation = Automatic process

---

## Pro Insight (Very Important for Hackathon)

Ye concept directly use hota hai:

* AI assistants (like ChatGPT)
* Customer support bots
* Multi-skill AI systems
* Autonomous workflows

👉 Agar tum isko samajh gaye:
You are not beginner anymore

---

## What’s Next?

Next step mein tum seekhoge:

👉 Memory ko aur powerful banana
👉 Agents ko long-term context dena

---
