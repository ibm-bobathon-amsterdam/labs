# Build Agentic Workflows Programmatically on watsonx Orchestrate Using IBM Bob

*A hands-on guide for creating automated invoice-processing agentic workflows using IBM Bob to generate code, tools, and configuration for watsonx Orchestrate*

**By** Allen Chan, Ahmed Azraq, Syeda Ameena Begum  
**Published:** 09 February 2026 · IBM Developer  
**Source:** [developer.ibm.com](https://developer.ibm.com/tutorials/build-programmatic-agentic-workflows-watsonx-orchestrate-bob/)

---

## Table of Contents

1. [Overview](#1-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [OPTIONAL – Configure watsonx Orchestrate MCP Servers](#4-optional--configure-watsonx-orchestrate-mcp-servers)
5. [Create a Bob Rule for Development Best Practices](#5-create-a-bob-rule-for-development-best-practices)
6. [Create the Implementation Plan and Agent Design](#6-create-the-implementation-plan-and-agent-design)
7. [Implement the Agent and the Agentic Workflow](#7-implement-the-agent-and-the-agentic-workflow)
8. [Deploy the Agentic Workflow and the Agent](#8-deploy-the-agentic-workflow-and-the-agent)
9. [Verify the Agent in watsonx Orchestrate](#9-verify-the-agent-in-watsonx-orchestrate)
10. [Summary and Next Steps](#10-summary-and-next-steps)

---

## 1. Overview

IBM watsonx Orchestrate (wxO) is an open and hybrid enterprise platform for agentic AI. It offers first-class multi-agent orchestration capabilities, integrated end-to-end security and governance, and observability capabilities for AI agents.

![watsonx Orchestrate – Open Agentic Framework](images/01-architecture-diagram.png)

The platform also offers multiple agent development tools: a low-code agent builder, pro-code development using the wxO Agent Development Kit (ADK), and integrated Langflow AI Builder.

![Agent development modes overview](images/02-architecture-table.png)

Instead of configuring components in the UI, developers can use the ADK to code all components, including agentic workflows — combining document processing, validation rules, schemas, and deployment steps in a repeatable, production-ready way.

In this tutorial, you will use **IBM Bob** as your AI development partner to automatically:

- Create the project structure
- Define a structured extraction schema
- Build a multi-step document-processing agentic workflow
- Validate the outputs
- Deploy both the agentic workflow and agent using wxO ADK

---

## 2. Architecture

You will build an agentic workflow that extracts structured data from airline invoices, removing manual data entry and improving processing efficiency.

![Invoice processing agentic workflow – architecture diagram](images/03-architecture-flow.png)

1. The user uploads an invoice document (PDF or image).
2. The **Expense Report Agent** on watsonx Orchestrate receives the document and starts the processing workflow using `groq/openai/gpt-oss-120b` as the LLM.
3. The **Invoice Processing Flow** retrieves the key-value pair (KVP) schema.
4. The KVP schema returns the list of fields to extract.
5. The **Extract Structured Data** component processes the invoice using the schema.
6. The **Structured JSON Output** contains all extracted invoice data.
7. The agent sends the formatted results to the user.

---

## 3. Prerequisites

- You have completed the [wxO – Bob environment setup guide](https://developer.watson-orchestrate.ibm.com) to prepare your Bob IDE properly.

---

## 4. OPTIONAL – Configure watsonx Orchestrate MCP Servers

> **Skip this section** if you already set up the wxO MCP servers using the environment setup guide.

Configure Bob to access the following watsonx Orchestrate MCP servers:

- **watsonx Orchestrate ADK Docs** – Queries the wxO ADK developer documentation.
- **watsonx Orchestrate ADK** – Gives Bob direct access to all ADK commands.

**Steps:**

1. Open the IBM Bob IDE with the `wxo-agentic-workflow` workspace active.
2. Create a new folder `.bob` to store all Bob-related configurations.
3. Create a new file `mcp.json` in the `.bob` folder. Replace `<your /absolute/path/to/project>` with your own path.

```json
{
  "mcpServers": {
    "watsonx-orchestrate-adk-docs": {
      "command": "uvx",
      "args": [
        "mcp-proxy",
        "--transport",
        "streamablehttp",
        "https://developer.watson-orchestrate.ibm.com/mcp"
      ]
    },
    "watsonx-orchestrate-adk": {
      "command": "uvx",
      "args": ["ibm-watsonx-orchestrate-mcp-server"],
      "env": {
        "WXO_MCP_WORKING_DIRECTORY": "<your /absolute/path/to/project>",
        "WXO_MCP_DEBUG": ""
      },
      "timeout": 300
    }
  }
}
```

![mcp.json configured in Bob IDE](images/04-mcp-json-config.png)

---

## 5. Create a Bob Rule for Development Best Practices

Create a Bob rule that captures best practices for development work with watsonx Orchestrate ADK. Bob rules apply across all modes and ensure Bob follows correct patterns when planning tasks, writing code, or using advanced features.

| File | Purpose |
|------|---------|
| `wxo-implementation-guide.md` (root) | Comprehensive reference guide Bob reads on demand |
| `.bob/rules/wxo-development.md` | Concise always-on rule applied automatically across all modes |

**Steps:**

1. Save `wxo-implementation-guide.md` to the root directory of your workspace.
2. Create a `rules` directory inside the `.bob` folder.
3. Create `wxo-development.md` in `.bob/rules/`. Copy the required content from the GitHub repository and save it.

![wxo-development.md rule file in Bob IDE](images/05-bob-rule-wxo-development.png)

---

## 6. Create the Implementation Plan and Agent Design

Provide Bob the agent requirements. Bob will then create the task plan and generate the agent architecture design.

> **Tip:** Be specific and clear in your prompts. Use the **enhance prompt** feature to improve your query with additional context and structure.

**Steps:**

1. Make sure you are in **Plan** mode and keep **auto-approval disabled**.

2. Provide Bob with the following agent requirements:

![Plan mode with agent requirements entered](images/06-plan-mode-prompt.png)

```text
Create a watsonx Orchestrate agent that will help a user create an expense report:

The agent will use a flow that:
1. Accept an uploaded document file
2. Extracts the expense fields below validated with KVP schema.
3. Return the output in structured JSON format

Required Fields to Extract:
  Invoice Information:
    - Invoice Date
    - Transaction Mode (e.g., Credit Card, Bank Transfer, Cash)
  Airline and Passenger Information (If airline invoice):
    - Airline Name / Passenger Name / Ticket Number / Ticket Date / Flight Details
  Hotel Information (If accommodation invoice):
    - Hotel Name / Customer Name / City
  Fee Information:
    - Base Fare / Charges / Taxes (with breakdown) / Total Amount / Currency
```

![Agent requirements submitted to Bob](images/07-bob-prompt-sent.png)

3. Bob will request access to read `wxo-implementation-guide.md`. Click **Approve**.

![Bob requests access to implementation guide](images/08-bob-approve-file.png)

4. Bob will request access to the watsonx Orchestrate ADK documentation MCP server. Review the task list and click **Approve**.

![Bob task list ready for approval](images/09-bob-task-list.png)

5. Bob may ask clarification questions. Choose the **simple approach**: single flow, default models, import script only, SaaS version.

![Bob clarification questions](images/10-bob-clarification.png)

6. Bob generates the implementation plan, architecture design, and workflow design. If Bob asks you to switch to code mode, **ignore this request**.

![Bob implementation plan complete](images/11-bob-plan-complete.png)

7. Switch to **Ask** mode and ask Bob: *"Show me the workflow diagram"*. Install the **Mermaid** extension to view it.

![Expense Extraction Flow – workflow diagram](images/12-workflow-diagram.png)

---

## 7. Implement the Agent and the Agentic Workflow

Ask Bob to generate the code and configuration needed to build the agent.

> **Important:** Thoroughly review the generated code to ensure it aligns with your intended functionality and requirements.

**Steps:**

1. Switch to **Advanced** mode so Bob can access both watsonx Orchestrate MCP servers.

2. Provide Bob with the following implementation instructions, then review the plan and click **Approve**.

![Advanced mode – implementation plan approved](images/13-advanced-mode-implement.png)

```text
Implement the approved plan and follow the below instructions:

Requirements:
  1. Create a native agent with this specific LLM model: groq/openai/gpt-oss-120b
  2. Build a document processing flow using docproc node.
  3. Define a KVP schema for the fields I need to extract.
  4. For simplicity include the KVP schema inline in the flow file.
  5. Ensure all imports are relative (using dot notation).

Important Implementation Details:
  - Use plain functions for schema helpers (no @tool decorator).
  - Use relative imports in all Python files.
  - Keep the flow simple with just a docproc node.
  - Use native agent type for better document handling.
  - Use JSON output format (not file reference).
```

3. Bob creates checkpoints so you can roll back if needed. Bob then creates the flow. Review the code and continue.

![Bob creates the expense extraction flow](images/14-bob-creates-flow.png)

4. Bob creates the agent YAML file with the agent configuration.

![Bob creates agent YAML configuration](images/15-bob-creates-agent-yaml.png)

5. Bob creates a script to import the workflow and the agent to watsonx Orchestrate.

![Bob creates the import-all.sh deployment script](images/16-bob-creates-import-script.png)

6. Bob creates a test script and documentation.

![Bob creates test script and README documentation](images/17-bob-creates-docs.png)

7. Bob verifies and confirms that the implementation is complete.

---

## 8. Deploy the Agentic Workflow and the Agent

Ask Bob to deploy the agentic workflow tool and agent YAML file by importing the script created in the previous step.

**Steps:**

1. Click the **watsonx extension tile** on the left sidebar and then click **Initialize the Workspace**.

![Initialize Workspace in the watsonx extension](images/18-initialize-workspace.png)

2. Wait for the **Environment Manager** to load your active environment. Click **Activate** to connect Bob to your environment. Enter your API key when prompted.

![Environment Manager showing active environment](images/19-environment-manager.png)

![API key prompt](images/20-api-key-prompt.png)

3. Give Bob the following deployment instruction:

```text
Run the import script to deploy the flow and agent to my watsonx Orchestrate
environment. If orchestrate command line is not installed, install
ibm-watsonx-orchestrate with pip.
```

![Bob receives the deployment instruction](images/21-bob-deploy-instruction.png)

4. Bob runs the import script to deploy the workflow and the agent.

![Bob runs the import script – flow and agent deployed](images/22-bob-runs-import.png)

---

## 9. Verify the Agent in watsonx Orchestrate

Confirm that the agentic workflow works correctly. Log in, check the agent configuration, and run a simple test.

**Steps:**

1. Log in to watsonx Orchestrate:
   - **Local environment:** Run `orchestrate chat start` in your workspace terminal. UI at `http://localhost:3000/chat-lite`
   - **IBM Cloud SaaS:** Log in to IBM Cloud → Resource list → AI/Machine Learning → Watson Orchestrate

![IBM Cloud resource list – finding the watsonx Orchestrate service](images/23-ibmcloud-resource-list.png)

![Launch watsonx Orchestrate from IBM Cloud](images/24-wxo-launch-button.png)

2. Go to **Manage Agents** and search for `expense_report_agent` created by Bob.

![Manage Agents – searching for expense_report_agent](images/25-manage-agents-search.png)

3. Confirm that the agentic workflow is attached and the agent uses the **GPT-OSS 120B – OpenAI (via Groq)** model.

![Agent configuration – workflow attached and LLM model confirmed](images/26-agent-config.png)

4. Test the agent by typing: *"Extract my invoices details from flight.pdf"*. Upload the PDF that Bob created and click **Send**.

![Testing the agent with a PDF invoice upload](images/27-test-agent-upload.png)

5. The agent returns all extracted invoice details in structured JSON format with a human-readable summary.

![Agent returns extracted invoice data in structured JSON](images/28-agent-json-result.png)

---

## 10. Summary and Next Steps

This tutorial showed how Bob automates the complete process of building and deploying agentic workflows for watsonx Orchestrate.

![Bob summary – all 10 tasks completed successfully](images/29-bob-all-tasks-complete.png)

### Completed Tasks

| Task | Description |
|------|-------------|
| ✓ Project Structure | Created complete directory structure with all necessary folders |
| ✓ Document Processing Flow | Implemented flow with inline KVP schema for expense extraction |
| ✓ Native Agent Configuration | Created agent using `groq/openai/gpt-oss-120b` LLM |
| ✓ Deployment Script | Created executable `import-all.sh` for easy deployment |
| ✓ Testing Script | Created `flow_main.py` for programmatic testing |
| ✓ Documentation | Created comprehensive README with architecture and workflow diagrams |
| ✓ Python Package Structure | Added all necessary `__init__.py` files |
| ✓ ADK Installation | Installed `ibm-watsonx-orchestrate` package |
| ✓ Flow Deployment | Successfully deployed `expense_extraction_flow` tool |
| ✓ Agent Deployment | Successfully deployed `expense_report_agent` |

### Related Resources

- [Using IBM Bob to build watsonx Orchestrate agents and MCP tools](https://developer.ibm.com/tutorials/build-agents-mcp-tools-watsonx-orchestrate-using-bob/)
- [Beginner's guide to multi-agent orchestration with watsonx Orchestrate](https://developer.ibm.com/articles/multi-agent-orchestration-watsonx-orchestrate/)
- [Try watsonx Orchestrate free trial](https://www.ibm.com/account/reg/us-en/signup?formid=urx-52753)

---

*This tutorial was published on IBM Developer · developer.ibm.com · © IBM Corporation 2026*
