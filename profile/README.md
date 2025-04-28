# Hatch! - Scientific Software Access for LLM-Powered Research

## About Hatch! 🥚
Hatch! is an open-source initiative focused on making scientific software accessible to Large Language Models (LLMs) through the Model Context Protocol (MCP). Our mission is to enable researchers to leverage the power of LLMs as scientific assistants with proper access to established scientific tools, databases, and resources, **all with proper citations**.

## Our Vision
We believe that LLMs can be transformed into powerful research assistants when they have proper, controlled access to scientific software and databases. Hatch! provides a standardized infrastructure where scientific tools can be wrapped as MCP servers, enabling LLMs to:

- **Provide proper citation for every tool and resource used**. 
- Execute computational tasks with scientific software
- Access and query scientific databases
- Process research data and generate insights

## The Hatch! Ecosystem
### Hatchling 🐥
Hatchling is our frontend application - a CLI-based chat interface that connects local LLMs (via Ollama) to MCP servers. It's the user-facing component that researchers interact with to access the entire Hatch! ecosystem.

#### Key features:

- Interactive chat interface with tool access management
- Support for local LLMs via Ollama
- Tool execution monitoring and timeout controls
- Automatic citation of all used scientific MCP servers hosted in Hatch! the LLM uses

### Scientific Domain Repositories (IN BUILDING)
We hope you people from all fields will gather here to share MCP server wrappers to the thousands of scientific software already published.
Come, and contribute to the repository that matches your software: 

- Hatch! Biology - MCP servers for bioinformatics tools (BLAST, UniProt, PubMed, etc.)
- Hatch! Chemistry - Chemical databases, molecular visualization, reaction prediction
- Hatch! Physics - Simulation tools, data analysis, and visualization
- Hatch! Mathematics - Computer algebra systems, statistical tools, and visualization
- Hatch! Computer Science - Code analysis, execution environments, and development tools
- Hatch! Engineering - CAD integration, simulation tools, and material databases

## Roadmap

1. Core Infrastructure Development (Current Phase)
- Stabilize Hatchling CLI interface
- Establish package architecture for MCP servers
- Develop versioning and dependency management

2. Scientific Domain Expansion
- Launch Hatch! Biology with essential bioinformatics tools
- Establish contribution guidelines for scientific software integration

3. Community Growth
- Support third-party MCP servers
- Deploy scientific domain repositories
- Develop educational resources for researchers
- Organize dev jams and hackathons

4. User Experience Enhancement
- Graphical user interface for Hatchling
- User-defined tool chains and workflows
- Integration with research notebooks and documentation tools

## Contributing

We are in the early stages and much is being setup internally for the time being.
However, if you're interested in contributing, using our tools in your research, or have questions about the project, please don't hesitate to reach out:

- Project Lead: Eliott Jacopin
- Email: eliott.jacopin@riken.jp

## License
Hatch! and Hatchling projects are released under the AGPLv3 License, though individual repositories licenses have their own specific licensing requirements based on the software they integrate with. Please see individual repositories for specific license information.
