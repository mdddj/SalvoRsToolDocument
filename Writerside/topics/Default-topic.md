# RustX Getting Started

RustX adds practical productivity tools for RustRover users working with **Salvo**, **Actix Web**, **SeaORM**, and common Rust-to-frontend code generation tasks.

## Install RustX

1. Open **Settings | Plugins** in RustRover.
2. Search for **RustX** in the JetBrains Marketplace.
3. Click **Install** and restart the IDE.

![Install RustX](install.png)

You can also open the Marketplace listing directly:

- [RustX on JetBrains Marketplace](https://plugins.jetbrains.com/plugin/24142-rustx)
- [RustX source code on GitHub](https://github.com/mdddj/SalvoRsTool)

## Before You Start

- Use **RustRover 2025.2** or newer.
- Open a Rust project that already includes the framework you want to work with, such as `salvo`, `actix-web`, or `sea-orm`.
- Wait until project indexing finishes after opening the project or updating dependencies.

## Salvo Endpoints

RustX can scan Salvo router definitions and show them in a dedicated tool window.

1. Open a project that contains Salvo routes.
2. Wait for RustX to finish scanning the project.
3. Open the **Salvo Endpoints** tool window from the right sidebar.
4. Click **Refresh** after route changes if you want to rescan immediately.
5. Use the context menu on an endpoint item to:
   - copy the API URL
   - generate an antd request snippet
   - jump to the route definition
   - jump to the handler implementation

RustX supports nested router chains, direct router-returning functions, and `push(...)` references more reliably in recent versions.

![Salvo Endpoints](https://raw.githubusercontent.com/mdddj/SalvoRsTool/main/images/salvo-api-window.png)

## Actix Web Endpoints

RustX also provides endpoint discovery for Actix Web projects.

1. Open an Actix Web project.
2. Open the **Actix Endpoints** tool window.
3. Browse detected routes and jump to their implementations.

![Actix Endpoints](https://raw.githubusercontent.com/mdddj/SalvoRsTool/main/images/actix-api-window.png)

## Code Generation from Rust Structs

RustX adds editor actions and intention actions for Rust structs.

You can generate:

- TypeScript interfaces
- Ant Design form code
- table column definitions
- Salvo DTO files
- Salvo router and service scaffolding

In most cases, you can trigger these actions from the editor popup menu or by placing the caret on a Rust struct.

## SeaORM Tools

RustX includes helper actions for common SeaORM workflows.

Available actions include:

- initialize SeaORM
- create migration files
- generate entities
- run migrate up or down
- run reset, fresh, or refresh
- convert JSON into SeaORM migration code

These tools are available from the project view actions and related plugin menus.

## Tips

- Re-run endpoint scanning after large router refactors.
- Keep route definitions reasonably explicit for the best parsing results.
- If a tool window is empty, first confirm that the project includes the expected framework dependency.
- If a generated result is not what you expect, refresh indexing and try again.

## Links

- [Documentation](https://mdddj.github.io/SalvoRsToolDocument)
- [Changelog](https://mdddj.github.io/SalvoRsToolDocument/changelog%E6%9B%B4%E6%96%B0%E6%97%A5%E5%BF%97.html)
- [Marketplace Listing](https://plugins.jetbrains.com/plugin/24142-rustx)
