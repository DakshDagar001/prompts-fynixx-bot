# Fynixx Bot

A powerful, modular, AI-ready Discord management bot built with TypeScript and discord.js.

## Overview

Fynixx Bot is designed to handle the full spectrum of Discord server administration. This repository contains the **Core Framework**, which provides the foundational engine for loading modules, commands, events, plugins, and connecting to services like PostgreSQL and Redis.

## Architecture

The bot follows Clean Architecture and SOLID principles, utilizing:
- **TypeScript 5.7+** for strict type safety
- **discord.js 14.x** for the Discord API
- **tsyringe** for Dependency Injection
- **Prisma** for database access (PostgreSQL)
- **Redis** for caching and distributed job queues (BullMQ)
- **Pino** for structured, high-performance logging
- **Zod** for schema validation

For more details, see the [Architecture Documentation](docs/architecture.md).

## Quickstart

### Prerequisites
- Node.js 22 LTS
- PostgreSQL 16
- Redis 7
- `pnpm` package manager

### Setup
1. Clone the repository
2. Run `pnpm install`
3. Copy `.env.example` to `.env` and fill in your values
4. Run `docker-compose up -d` to start the local database and cache
5. Run `pnpm prisma:push` to sync the database schema
6. Run `pnpm dev` to start the bot in development mode

## Feature Modules

*(Coming in Phase 3)*

Feature modules (like Moderation, Tickets, AI) are self-contained and located in `src/modules/`. They automatically plug into the Core Framework's Command and Event loaders.

## Contributing

Please read the [Development Guide](docs/development-guide.md) before making changes. All commits must follow Conventional Commits guidelines.
