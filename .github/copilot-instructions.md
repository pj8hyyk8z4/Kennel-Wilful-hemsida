# Copilot instructions

## Repository scope

This is a Swedish-language documentation repository for describing how the Kennel Wilful website is structured. The current repository contains no website implementation, package manifest, or build configuration. Do not assume an application, framework, or deployment workflow exists until it is added to the repository.

## Commands

No build, test, lint, or single-test commands are configured at present.

## MCP configuration

`.github/mcp.json` provides the shared Playwright MCP server for browser inspection and testing when Copilot is working in a trusted checkout.

## Documentation conventions

- Keep repository documentation in Swedish, matching `README.md`.
- Treat `README.md` as the entry point for the website-structure documentation. Extend it with the relevant architectural detail as the documentation grows.
- Add tooling instructions only alongside the tooling they describe, and update this file when a build, test, or lint workflow is introduced.
