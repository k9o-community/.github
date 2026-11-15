# Kilimanjaro community

Kilimanjaro is a modular developer platform for building secure enterprise applications.
You define AI agents, functions and data pipelines on the platform.
The SDKs let you deploy and invoke them, read and write your data, publish to and subscribe to streams,
sign users in, and encrypt with keys you hold.

## Architecture at a glance

![Architecture at a glance, steps 1 to 7: invoke calls enter at Ingress (1) and reach an extension (2) that runs in a Firelock sandbox on Bun or Wasmtime. The sandbox has no network of its own: all guest egress goes through one auditable vsock channel to the Decision Oracle (3), Warden, which evaluates each call and escalates to a human reviewer (4) when needed. Allowed calls go to the Credentials Oracle (5), which brokers all credentials with Kibo (6), so the extension never holds credentials. Calls leave through Egress (7), only to allow-listed endpoints.](https://raw.githubusercontent.com/k9o-community/.github/main/profile/extension-framework-architecture.svg)

An extension runs in an isolated sandbox with no network of its own, so everything it does passes through points the platform controls:

1. **Ingress.** A call to an extension enters the platform here.
2. **The extension.** Your code runs in a [Firelock](https://firelock-sandbox.github.io/) sandbox on Bun or Wasmtime. The sandbox has no network of its own. Everything the extension sends out leaves through one auditable channel.
3. **Decision Oracle.** Warden, the Decision Oracle, evaluates every call the extension makes. External agents that submit tool calls through the platform's MCP interface meet the same checks.
4. **Human review.** When a call needs a person's approval, the Decision Oracle escalates it to a human reviewer.
5. **Credentials Oracle.** A call the Decision Oracle allows goes to the Credentials Oracle, which brokers every credential the call needs.
6. **Kibo.** The Credentials Oracle works with Kibo, which holds the credentials. The extension never holds a credential.
7. **Egress.** The call leaves the platform here, and only to endpoints on an allow-list.

This organization holds extensions, examples and tools built by the community for Kilimanjaro.

## What you can do here

- **Extend the platform.** Build an AI agent, function, or data pipeline that adds a capability to Kilimanjaro, and share it so others can install it.
- **Learn from working code.** Read examples that show how to use the SDKs, the CLI and the platform's building blocks (Keep, Pulse, Gate and Kibo) in a real application.
- **Get your tool in front of users.** Publish a tool, a template or an integration that helps other Kilimanjaro developers.
- **Shape what comes next.** Open an issue to ask for a change, report a problem or propose an idea.

## Start here

1. **Build against the platform.** Install an official SDK or the CLI from [github.com/k9o-platform](https://github.com/k9o-platform). The README of each SDK takes you from install to a first authenticated call, and shows how the platform fits together.
2. **Read the guides** in the Developer Hub: <https://docs.kilimanjaro.dev>.
3. **Share your work.** Open a pull request on an existing repository, or ask in an issue for a new one. See [CONTRIBUTING](https://github.com/k9o-community/.github/blob/main/CONTRIBUTING.md) for how to propose a change and what a good pull request includes.

## Links

- Website: <https://kilimanjaro.dev>
- Documentation / Developer Hub: <https://docs.kilimanjaro.dev>
- Official SDKs and CLI: <https://github.com/k9o-platform>

## Help

Questions and bugs: open an issue on the repository concerned, or email <engineering@kilimanjaro.dev>.

To report a security problem, follow [SECURITY](https://github.com/k9o-community/.github/blob/main/SECURITY.md).
