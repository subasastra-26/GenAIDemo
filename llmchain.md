import os
from dotenv import load_dotenv

from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate

# Load API key
load_dotenv()

# LLM
llm = ChatOpenAI(
    temperature=0.3,
    api_key=os.getenv("OPENAI_API_KEY")
)

# Prompt
# Prompt (IMPORTANT: must be defined BEFORE chain)
prompt = ChatPromptTemplate.from_template("""
You are a professional multilingual translator.

Supported languages:
Tamil, English, Hindi, Telugu, Tanglish (Tamil written in English letters)

Task: {mode}

Rules:
- Translate naturally (human meaning, not word-by-word)
- Keep tone correct
- Tanglish → understand Tamil meaning then convert to English
- Output only translated text

Input:
{text}
""")
# Chain using LCEL (modern LangChain style)
chain = prompt | llm

def translate_text(text, mode):
    response = chain.invoke({"text": text, "mode": mode})
    return response.content
