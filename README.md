🧠 Arabic-Only AI Assistant (via OpenRouter + Deepseek)
This project sets up an AI Assistant that only responds in Arabic, powered by the deepseek/deepseek-prover-v2:free model through OpenRouter API. It is designed to run in Google Colab using openai-agents and AsyncOpenAI.

🚀 Features
Uses OpenRouter to access third-party AI models

Sets strict instruction boundaries (Arabic-only replies)

Asynchronous execution with asyncio

Simple and minimal example using the Agent SDK

🧩 Tech Stack
Python (async/await)

OpenRouter

Deepseek Prover Model (deepseek/deepseek-prover-v2:free)

openai-agents

Google Colab integration

🔧 Setup (Google Colab)
python
Copy
Edit
# Install the agent SDK
!pip install -Uq openai-agents

# Apply async loop patch for Colab
import nest_asyncio
nest_asyncio.apply()

# Load API key securely from Colab
from google.colab import userdata
OPENROUTER_API_KEY = userdata.get("DEEPSEEK_KEY")

# OpenRouter API setup
from openai import AsyncOpenAI
BASE_URL = "https://openrouter.ai/api/v1"
MODEL = "deepseek/deepseek-prover-v2:free"
client = AsyncOpenAI(api_key=OPENROUTER_API_KEY, base_url=BASE_URL)
📜 Run the Assistant
python
Copy
Edit
from agents import Agent, OpenAIChatCompletionsModel, Runner, set_tracing_disabled
import asyncio

set_tracing_disabled(disabled=True)

async def main():
    agent = Agent(
        name="Assistant",
        instructions="You can only respond in arabic",
        model=OpenAIChatCompletionsModel(model=MODEL, openai_client=client)
    )
    result = await Runner.run(agent, "what is your name?")
    print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
🔐 Notes
Replace DEEPSEEK_KEY in userdata.get() with your actual variable name.

Make sure you’ve set up OpenRouter API access and your model is authorized for use.
