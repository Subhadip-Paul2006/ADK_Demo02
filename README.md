# Demo03 - Team Agent Tutorial

Yeh project Google ADK par based ek step-by-step tutorial hai. Ismein tum ek simple weather agent se start karke multi-agent team, session memory, input safety, aur tool safety tak ka complete flow dekhte ho.

Simple line mein:

User -> Runner -> Root Agent -> Sub-Agent / Tool -> Response

## Is Project Mein Kya Hai

Is repo mein 2 cheezein saaf dikhayi gayi hain:

1. Tutorial notes in markdown files.
2. Working Python example in `my_agent_v3`.

### Main Python Files

- `my_agent_v3/agent.py` - basic starter agent example.
- `my_agent_v3/team_agent.py` - full tutorial script with weather, greeting, farewell, memory, and guardrails.
- `my_agent_v3/__init__.py` - package entry point.

## Tutorial Flow

Markdown docs ko order mein padhoge to complete story samajh aati hai:

1. `Team_Agent_BasicWeatherLookUp.md`
   - basic weather agent
   - agent, tool, session, runner ka meaning
2. `Team_Agent_GreetingsFarewells.md`
   - multiple agents
   - root agent aur sub-agents
   - automatic delegation
3. `Team_Agent_MemoryPersonalization.md`
   - session state
   - user preference store karna
   - personalized weather output
4. `Team_Agent_AddingSafetyInputGuardrail.md`
   - `before_model_callback`
   - user input ko LLM se pehle block karna
5. `Team_Agent_AddingSafetyTool.md`
   - `before_tool_callback`
   - tool arguments ko verify karke unsafe call rokna

## Kaise Sochna Hai Is System Ko

Sabse important mental model yeh hai:

- Agent = brain / decision maker
- Tool = worker / actual kaam karne wala function
- Session State = memory
- Runner = engine jo sab chalata hai

### Team Agent Model

Root agent manager ki tarah kaam karta hai. Wo query ko samajhkar decide karta hai:

- khud weather handle kare
- greeting agent ko bheje
- farewell agent ko bheje

### Memory Model

Session state se agent yaad rakhta hai:

- user ko Celsius chahiye ya Fahrenheit
- last city kya thi
- last response kya tha

### Safety Model

Do safety layers use hoti hain:

- Input guardrail: user message ko LLM se pehle check karta hai
- Tool guardrail: tool chalne se pehle arguments ko verify karta hai

## `my_agent_v3/team_agent.py` Ka Real Flow

Ye file tutorial ko ek long, readable script ki tarah build karti hai. Ismein multiple stages hain:

### 1. Weather Tool

`get_weather(city)` ek simple weather tool hai jo city ke naam par mock/current weather deta hai.

### 2. Greeting and Farewell Tools

- `say_hello(name)` greeting deta hai
- `say_goodbye()` farewell deta hai

### 3. Root Agent v2

Root agent weather ko handle karta hai aur sub-agents ko delegate karta hai.

### 4. Stateful Root Agent v4

Yahan `get_weather_stateful(city, tool_context)` use hota hai.

- ye session state read karta hai
- Celsius/Fahrenheit ke hisaab se output convert karta hai
- last checked city ko state mein save karta hai

### 5. Input Guardrail v5

`block_keyword_guardrail(...)` check karta hai ki user input mein `BLOCK` word hai ya nahi.

- agar word milta hai, LLM call stop ho jaati hai
- agar nahi milta, normal flow chalta hai

### 6. Tool Guardrail v6

`block_paris_tool_guardrail(...)` weather tool ko Paris ke case mein block karta hai.

- allowed cities execute hoti hain
- blocked city ke liye custom error response return hota hai

## Important Learning Points

### Description Field Bahut Important Hai

Sub-agent ka `description` root agent ke liye hint hota hai. Isi se wo decide karta hai ki query kisko deni hai.

### `output_key` Kya Karta Hai

`output_key="last_weather_report"` final agent response ko session state mein save kar deta hai.

### Guardrail Return Rules

- `before_model_callback` agar `LlmResponse` return kare to LLM skip ho jaata hai.
- `before_tool_callback` agar `dict` return kare to actual tool skip ho jaata hai.

## Architecture Diagram

```text
User
  ↓
Runner
  ↓
Root Agent
  ↓
┌───────────────┬───────────────┐
↓               ↓               ↓
Weather      Greeting       Farewell
Tool/Sub      Agent          Agent
Agent
  ↓               ↓               ↓
Response merge / final answer
```

## Why This Project Is Useful

Ye project sirf weather bot nahi hai. Ye dikhata hai ki real AI assistant kaise build hota hai:

- multiple skills
- delegation
- memory
- safety controls
- clean orchestration

Hackathon, portfolio, aur learning ke liye yeh strong foundation hai.

## Setup Notes

Project ko chalane se pehle tumhe usually ye chahiye hota hai:

- Python environment
- Google ADK related dependencies
- weather example ke liye `requests`
- valid API key / model setup

`.env` file mein secrets rakho, git mein commit mat karo.

## How To Read This Repo

Agar tum beginner ho, recommended order yeh hai:

1. `Team_Agent_BasicWeatherLookUp.md`
2. `Team_Agent_GreetingsFarewells.md`
3. `Team_Agent_MemoryPersonalization.md`
4. `Team_Agent_AddingSafetyInputGuardrail.md`
5. `Team_Agent_AddingSafetyTool.md`
6. `my_agent_v3/team_agent.py`

## Short Summary

Ye repo ek complete ADK learning path hai:

- basic weather agent
- team of agents
- memory-based personalization
- input safety
- tool safety

Agar tum is flow ko samajh gaye, to tum simple chatbot se aage ek proper agent system build kar sakte ho.
