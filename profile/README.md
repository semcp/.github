# `semcp` 

"Secure Execution for MCP Agents 🤖"

AI Agents with MCP tools are becoming increasingly powerful and popular - but with that power comes security risks. These agents can execute arbitrary code or access sensitive resources. Without proper safeguards, attackers can exploit prompt injection and model-context poisoning to subvert agent behavior and misuse tools. For example, an attacker could hide malicious instructions in retrieved data or tool description that an LLM follows faithfully - causing data exfiltration or the entire system being compromised.

The goal of `semcp` organization is to build a secure foundation for the Agent and MCP ecosystem. I'd like to explore the following areas:

- Sandboxing options for MCP tools.
- Enforcable security policies for agents.
- A secure agent system to incorporate best security practices to protect against prompt injection.

## Projects

- [semcp](https://github.com/semcp/semcp): a kit for running MCP servers in docker containers, providing drop-in replacement for `npx` or `uvx`, specifically designed for MCP servers.
- [mcp-sinstaller](https://github.com/semcp/mcp-sinstaller): a MCP server to install and containerize other MCP servers.
- [MCP Capability Policy](https://github.com/semcp/policy-mcp-rs): MCP Capability Policy specification and library.
- [🐪 Dromedary](https://github.com/semcp/dromedary): a capability-based agent system designed to protect against prompt injection.

Besides docker containers, we are also exploring the following sandboxing options:

- **Lightweight VMs**: microVM such as [Hyperlight](https://github.com/hyperlight-dev/hyperlight) can boot in milliseconds and supports thousands of microVMs per host. It provides the hardware-level isolation between the tools and the host that runs the agent. For example, the [E2B](https://github.com/e2b-dev/e2b) project spawns each untrusted code interpreter in a Firecracker microVM, giving the LLM a “small cloud VM” to execute in. This could be ideal for running MCP servers on desktop (with hypervisor-supported hardware), cloud providers or edge devices, though it comes with overhead in memory and latency.

- **WebAssembly**: To get even faster startup time, we can compile MCP servers to [WebAssembly](https://webassembly.org/) and run them in [WASI](https://wasi.dev/)-compatible runtimes like [wasmtime](https://wasmtime.dev/) for software-defined isolation. The modular design of WASI allows the host to easily implement proxy-like HTTP filters without a sidecar container. The  downside of this is the lack of a more mature ecosystem in the guest side to support mainstream programming languages such as Python and JavaScript to be able to compile to Wasm.

