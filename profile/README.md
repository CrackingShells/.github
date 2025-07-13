# Hatch! - Scientific Software Access for LLM-Powered Research

![Hatch Logo](../resources/images/cs_wide_dark_bg_Hatchling.png)

## About Cracking Shells 🥚
**Cracking Shells** is an open-source initiative focused on making scientific software accessible to Large Language Models (LLMs) through the Model Context Protocol (MCP). Our mission is to enable researchers to leverage the power of LLMs as scientific assistants with proper access to established scientific tools, databases, and resources, **all with proper citations**.

## Our Vision
We believe that LLMs can be transformed into powerful research assistants when they have proper, controlled access to scientific software and databases. **Cracking Shells** provides a standardized infrastructure where scientific tools can be wrapped as MCP servers, enabling LLMs to:

- **Provide proper citation for every tool and resource used**. 
- Execute computational tasks with scientific software
- Access and query scientific databases
- Process research data and generate insights

## The Cracking Shells Ecosystem

### Hatch!
**[Hatch!](https://github.com/CrackingShells/Hatch)** is the package manager for MCP servers packages hosted on the ecosystem called _Hatch! Packages_. Such packages notably enable declaring dependencies of the MCP servers as well as the citations an LLM must report when using an MCP server. It also handles automatically all the installation and organization of the python environments necessary for the dependencies to be installed.

### Hatchling 🐥
**[Hatchling](https://github.com/CrackingShells/Hatchling)** is our frontend application - a CLI-based chat interface that connects local LLMs (via Ollama) to MCP servers. It's the user-facing component that researchers interact with to access the entire **Cracking Shells** ecosystem.

#### Key features:

- Interactive chat interface with tool access management
- Support for local LLMs via Ollama
- Tool execution monitoring and timeout controls
- Automatic citation of all used scientific MCP servers managed by _Hatch!_ the LLM uses

### Scientific Domain Repositories (IN BUILDING)
We hope you people from all fields will gather here to share MCP server wrappers to the thousands of scientific software already published.
Come, and contribute to the repository that matches your software:

- Cracking Biology - MCP servers for bioinformatics tools (BLAST, UniProt, PubMed, etc.)
- Cracking Chemistry - Chemical databases, molecular visualization, reaction prediction
- Cracking Physics - Simulation tools, data analysis, and visualization
- Cracking Mathematics - Computer algebra systems, statistical tools, and visualization
- Cracking Computer Science - Code analysis, execution environments, and development tools
- Cracking Engineering - CAD integration, simulation tools, and material databases

## Roadmap

1. **(Current)** Core Infrastructure Development (Current Phase)
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
