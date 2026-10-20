


# robinhood-chatgpt-mcp-sandbox
Educational framework and security guide for connecting Robinhood Agentic Trading to ChatGPT via MCP

# 🤖 Robinhood Agentic Trading & ChatGPT MCP Sandbox

An educational framework and prompt engineering guide for safely connecting **Robinhood's Agentic Trading MCP** to **ChatGPT** with strict human-in-the-loop guardrails.

---

## 📌 Overview

This project explores the integration between Robinhood's dedicated Agentic Trading sub-accounts and OpenAI's ChatGPT using the Model Context Protocol (MCP). 

### Key Features Explored:
- **Read-Only Portfolio Intelligence:** Querying balances, holdings, and execution history in natural language.
- **Strict Guardrails:** Keeping `Trade Approvals = ON` so the AI acts purely as an analyst/co-pilot.
- **Account Isolation:** Restricting AI execution solely to a dedicated, small-capital test sub-account.

---

## 🔒 Security & Privacy Considerations (Crucial)

Before connecting live brokerages to LLMs, understand the data boundaries:

1. **Data Exposure:** Passing account context via MCP exposes your buying power, balances, and positions to the AI provider's environment (governed by OpenAI's privacy terms).
2. **Data Retention:** Turn off model training in ChatGPT settings (`Settings -> Data Controls -> Improve the model for everyone = OFF`) to keep financial context private.
3. **Execution Isolation:** Main portfolio cash remains safe—the agent can only touch funds intentionally moved into the **Dedicated Agentic Sub-Account**.

---

## 🚀 Setup & Connection Guide

### 1. Robinhood Mobile Setup
- Navigate to **Account -> Agents -> Agentic Trading**.
- Create a **Dedicated Agent Account** and fund it with nominal test capital ($20–$50).
- Ensure **Trade Approvals** remains **ENABLED** in settings.
- **Hard Firewall:** As shown above (`vinaysqqq`), the dedicated sub-account is funded with a nominal test balance ($5.00)[cite: 3].
- **Zero Cross-Account Spillover:** The connected LLM agent can only query or trade funds within this isolated container. Primary investment accounts remain separated.
- **Trade Approvals = ON:** Manual confirmation is required by default before any order is submitted to the market.

- <img width="1075" height="661" alt="image" src="https://github.com/user-attachments/assets/552a980b-443d-405b-9c86-df79efc3978a" />


### 2. ChatGPT Desktop Setup
1. Enable **Developer Mode** in ChatGPT Settings.
2. Under **Plugins / Custom Connectors**, click `Add custom MCP server`.
3. Enter URL: `https://agent.robinhood.com/mcp/trading`
4. Complete Robinhood OAuth authentication.

<img width="1046" height="242" alt="c0361a14-7418-4af0-bbf9-da188e780c2e" src="https://github.com/user-attachments/assets/7ebefab4-db72-4710-a92c-99c6b62507ea" />
<img width="605" height="666" alt="image" src="https://github.com/user-attachments/assets/3e8fa98e-fcf6-42e1-aac4-5c9b35a75c02" />
---
## 💬 Guardrail System Prompt Template

To enforce human-in-the-loop oversight and ensure ChatGPT operates strictly in an analytical co-pilot role when connected to Robinhood, paste the following prompt as your initial session message or under **ChatGPT Settings -> Personalization -> Custom Instructions**:

I am connecting my @Robinhood Agent. Please adopt the following system instructions for this entire session:

ROLE: Research & Technical Co-Pilot Assistant

RULES:
1. NEVER submit automated orders without explicit manual preview/approval cards.
2. Operate strictly in read-only mode unless requested otherwise.
3. Always display Max Risk, Limit Price, and Ticker before prompting for approval.
