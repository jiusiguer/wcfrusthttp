# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Tauri-based desktop application that provides an HTTP client for WeChatFerry, a tool for interacting with WeChat. The application consists of:

1. A Rust backend that interfaces with WeChat through DLLs
2. A Vue.js frontend with Element Plus UI components
3. An HTTP API server built with Warp
4. WebSocket support for real-time messaging

## Architecture

- **Frontend**: Vue 3 with TypeScript, Element Plus UI library, and Ace Editor for log viewing
- **Backend**: Rust with Tauri framework for desktop app integration
- **Communication**: HTTP API using Warp, with optional WebSocket support
- **Messaging**: Event-driven architecture with message buses for handling WeChat events
- **Data**: Protocol Buffers for serialization, SQLite database access

## Common Development Tasks

### Building and Running

```bash
# Install dependencies
pnpm install

# Run in development mode
pnpm tauri dev

# Build for production
pnpm tauri build

# Frontend development server only
pnpm dev

# Frontend production build only
pnpm build
```

### Rust Development

```bash
# Run with more debug information
RUST_BACKTRACE=full RUST_LOG=debug cargo tauri dev

# Check code without building
cargo check

# Run tests (if any)
cargo test
```

### API Documentation

Once running, the API documentation is available at:
- http://localhost:10010/swagger/ (Swagger UI)
- http://localhost:10010/api-doc.json (OpenAPI JSON)

## Project Structure

- `src/` - Vue frontend code
- `src-tauri/` - Rust backend code
- `src-tauri/src/` - Main Rust source files
- `src-tauri/src/wcferry/` - WeChat integration layer
- `src-tauri/src/service/` - Service implementations (HTTP, WebSocket, etc.)
- `src-tauri/src/handler/` - Event handlers for different message types
- `src/components/` - Vue components
- `src/router/` - Vue router configuration
- `src/store/` - Pinia state management

## Key Components

1. **WeChat Service** (`src-tauri/src/wcferry/`) - Core WeChat integration using Protocol Buffers
2. **HTTP Server** (`src-tauri/src/service/http_server_service.rs`) - Warp-based HTTP API
3. **Event System** (`src-tauri/src/handler/`) - Message bus architecture for handling events
4. **Frontend** (`src/`) - Vue-based UI with log viewer and configuration panels
5. **Global State** (`src-tauri/src/service/global_service.rs`) - Application-wide state management

## Configuration

The application uses `config.json5` for runtime configuration:
- HTTP server port
- Callback URLs
- WebSocket URL
- File storage directory
- Message filtering options

## Dependencies

- **Rust**: tokio, warp, serde, prost (Protocol Buffers)
- **Frontend**: Vue 3, Element Plus, Ace Editor
- **Build**: Tauri CLI, Vite, TypeScript

## Testing

The application is primarily tested through:
1. Manual testing via the UI
2. API testing using the Swagger interface
3. Integration testing with actual WeChat instances

Note that this is a desktop application for interacting with WeChat, and testing requires a valid WeChat installation.