# ADK_Demo02

* `name`: A unique identifier for this agent (e.g., "weather\_agent\_v1").
* `model`: Specifies which LLM to use (e.g., `MODEL_GEMINI_2_5_FLASH`). We'll start with a specific Gemini model.
* `description`: A concise summary of the agent's overall purpose. This becomes crucial later when other agents need to decide whether to delegate tasks to *this* agent.
* `instruction`: Detailed guidance for the LLM on how to behave, its persona, its goals, and specifically *how and when* to utilize its assigned `tools`.
* `tools`: A list containing the actual Python tool functions the agent is allowed to use (e.g., `[get_weather]`).
