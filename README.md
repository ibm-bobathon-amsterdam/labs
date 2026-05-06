# IBM Bobathon Amsterdam Labs

Welcome to the IBM Bobathon Amsterdam Labs repository! This collection of hands-on labs demonstrates how to leverage IBM Bob as an AI development partner to build enterprise-grade solutions.

## About IBM Bob

IBM Bob is an AI-powered development assistant that helps developers create, deploy, and manage applications more efficiently. Bob can generate code, create documentation, design architectures, and automate deployment workflows.

---

## Available Labs

### [Lab 2: Build Agentic Workflows Programmatically on watsonx Orchestrate Using IBM Bob](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/)

**Focus**: Programmatic agent development using IBM Bob and watsonx Orchestrate ADK

**🚀 [START LAB 2 NOW →](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/wxo-bob-lab.md)**

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
- Complete the [Prerequisites setup guides](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/Prerequisites/) first
- IBM Bob IDE installed and configured
- watsonx Orchestrate access (local or IBM Cloud SaaS)
- Python environment with pip

**Lab Materials:**
- 📄 [Complete Tutorial](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/wxo-bob-lab.md) (336 lines, 10 sections)
- 📖 [Lab README](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/README.md)
- 🖼️ 29 step-by-step screenshots

[**Start Lab 2 →**](Lab%202%20-%20Build%20Agentic%20Workflows%20Programmatically%20on%20watsonx%20Orchestrate%20Using%20IBM%20Bob/)

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
└── Lab 2 - Build Agentic Workflows Programmatically on watsonx Orchestrate Using IBM Bob/
    ├── Prerequisites/             # Setup guides (complete first)
    │   ├── environment-setup.md
    │   └── watsonx-orchestrate-signup.md
    ├── wxo-bob-lab.md            # Complete tutorial
    └── images/                    # 29 screenshots
```

## Support and Resources

- [IBM Developer](https://developer.ibm.com)
- [watsonx Orchestrate Documentation](https://developer.watson-orchestrate.ibm.com)
- [IBM Bob Documentation](https://www.ibm.com/products/bob)

## Contributing

This repository is maintained for educational purposes. For questions or feedback, please contact the lab authors.

---

**Happy Learning! 🚀**