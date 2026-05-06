# IBM Bobathon Amsterdam Labs

Welcome to the IBM Bobathon Amsterdam Labs repository! This collection of hands-on labs demonstrates how to leverage IBM Bob as an AI development partner to build enterprise-grade solutions.

## About IBM Bob

IBM Bob is an AI-powered development assistant that helps developers create, deploy, and manage applications more efficiently. Bob can generate code, create documentation, design architectures, and automate deployment workflows.

## Prerequisites

Before starting any lab, complete the setup guides in the [Prerequisites](Prerequisites/) folder:

### 📋 [Setup Guides](Prerequisites/)

1. **[Environment Setup](Prerequisites/environment-setup.md)** (30-45 min)
   - Install Python 3.11+, IBM Bob IDE, and watsonx Orchestrate ADK
   - Configure MCP servers for Bob integration

2. **[watsonx Orchestrate Signup](Prerequisites/watsonx-orchestrate-signup.md)** (15-20 min)
   - Create IBM Cloud account
   - Provision watsonx Orchestrate service
   - Generate API credentials and configure ADK

**👉 [Start with Prerequisites →](Prerequisites/)**

---

## Available Labs

### [Lab 2: Build Agentic Workflows with watsonx Orchestrate](Lab2%20-%20watsonx%20Orchestrate%20/)

**Focus**: Programmatic agent development using IBM Bob and watsonx Orchestrate ADK

**🚀 [START LAB 2 NOW →](Lab2%20-%20watsonx%20Orchestrate%20/wxo-bob-lab.md)**

**What You'll Learn:**
- Configure Bob with Model Context Protocol (MCP) servers for watsonx Orchestrate
- Use Bob's Plan mode to design agent architectures
- Generate complete agentic workflows automatically
- Deploy AI agents to watsonx Orchestrate
- Build document processing workflows with structured data extraction

**What You'll Build:**
An automated **Expense Report Agent** that processes invoice documents (PDFs/images) and extracts structured data including:
- Invoice information (date, transaction mode)
- Airline/passenger details (ticket, flight info)
- Hotel information (name, customer, city)
- Fee breakdown (base fare, charges, taxes, total)

**Key Technologies:**
- IBM Bob (AI development assistant)
- watsonx Orchestrate (Enterprise agentic AI platform)
- watsonx Orchestrate ADK (Agent Development Kit)
- Model Context Protocol (MCP)
- LLM: `groq/openai/gpt-oss-120b`

**Time Estimate**: 60-75 minutes

**Prerequisites:**
- IBM Bob IDE installed and configured
- watsonx Orchestrate access (local or IBM Cloud SaaS)
- Python environment with pip

**Lab Materials:**
- 📄 [Complete Tutorial](Lab2%20-%20watsonx%20Orchestrate%20/wxo-bob-lab.md) (336 lines, 10 sections)
- 📖 [Lab README](Lab2%20-%20watsonx%20Orchestrate%20/README.md)
- 🖼️ 29 step-by-step screenshots

[**Start Lab 2 →**](Lab2%20-%20watsonx%20Orchestrate%20/)

---

## Getting Started

1. Choose a lab from the list above
2. Navigate to the lab directory
3. Read the lab's README for an overview
4. Follow the step-by-step tutorial
5. Complete the hands-on exercises

## Repository Structure

📁 **[View Complete Repository Structure →](REPOSITORY-STRUCTURE.md)**

Each lab includes:
- **README.md**: Lab overview, objectives, and prerequisites
- **Tutorial**: Detailed step-by-step instructions
- **Images**: Screenshots and diagrams
- **Sample Code**: Reference implementations (where applicable)

```
bobathon-amsterdam-labs/
├── Prerequisites/              # Setup guides (complete first)
│   ├── environment-setup.md
│   └── watsonx-orchestrate-signup.md
└── Lab2 - watsonx Orchestrate/ # Agentic workflows lab
    ├── wxo-bob-lab.md         # Complete tutorial
    └── images/                 # 29 screenshots
```

## Support and Resources

- [IBM Developer](https://developer.ibm.com)
- [watsonx Orchestrate Documentation](https://developer.watson-orchestrate.ibm.com)
- [IBM Bob Documentation](https://www.ibm.com/products/bob)

## Contributing

This repository is maintained for educational purposes. For questions or feedback, please contact the lab authors.

---

**Happy Learning! 🚀**