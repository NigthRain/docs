---
title: Agent设计模式(五):工具使用 - 知乎
author: 数据与AI爱好者
source_url: https://zhuanlan.zhihu.com/p/1960674438824592130?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-16 11:10
content_type: Article
vote_up_count: 26
comment_count: 4
collected_at: 2026-08-18 10:32:49
index: 197/314
---

# Agent设计模式(五):工具使用 - 知乎

> 数据与AI爱好者 | 2026-03-16 11:10

来源: https://zhuanlan.zhihu.com/p/1960674438824592130?utm_medium=openapi_platform&utm_source=1a2112

---

import os, getpass import asyncio import nest_asyncio from typing import List 
from dotenv import load_dotenv 
import logging 
from langchain_google_genai import ChatGoogleGenerativeAI from langchain_core.prompts import ChatPromptTemplate from langchain_core.tools import tool as langchain_tool 
from langchain.agents import create_tool_calling_agent, AgentExecutor 
# UNCOMMENT 
# Prompt the user securely and set API keys as an environment variables 
os.environ["GOOGLE_API_KEY"] = getpass.getpass("Enter your Google API 
key: ") os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter your OpenAI API 
key: ") 
try: 
# A model with function/tool calling capabilities is required. 
temperature=0) except Exception as e: llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash", print(f"✅ print(f" Language model initialized: {llm.model}") Error initializing language model: {e}") 
llm = None 
# --- Define a Tool --- 
@langchain_tool 
def search_information(query: str) -> str: 
""" 
find answers to phrases Provides factual information on a given topic. Use this tool to 

