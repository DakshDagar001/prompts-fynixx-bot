# Development Guide

Welcome to the Fynixx Bot development team! This guide explains our workflow, conventions, and how to build new features.

## Project Structure

The project is divided into three main areas:
- `src/core/`: The core engine (command loader, event bus, DI container, database connections). **Do not modify** without discussing with the architecture team.
- `src/modules/`: Feature modules (moderation, tickets, etc.). This is where 90% of development happens.
- `src/shared/`: Shared utilities, types, and constants.

## Adding a New Module

To add a new feature, create a new directory in `src/modules/` (e.g., `src/modules/tickets/`).

Your module must export an `IModule` implementation in its `index.ts`. The Core Framework will automatically discover and load it during the bot's startup sequence.

```typescript
// src/modules/example/index.ts
import { IModule, IModuleMeta } from '../../core/module/interfaces/IModule.js';

export class ExampleModule implements IModule {
  public meta: IModuleMeta = {
    name: 'example',
    description: 'An example module',
    version: '1.0.0'
  };

  public getCommands() { return []; }
  public getEventHandlers() { return []; }
  public async onLoad() {}
  public async onReady() {}
  public async onShutdown() {}
}
```

## Dependency Injection

We use `tsyringe` for dependency injection. Always use the `@injectable()` decorator on your classes.

```typescript
import { injectable } from 'tsyringe';
import { Logger } from '../../core/logger/Logger.js';

@injectable()
export class ExampleService {
  constructor(private readonly logger: Logger) {}
  
  public doSomething() {
    this.logger.info('Doing something...');
  }
}
```

## Logging

Never use `console.log`. Always inject the `Logger` service and use its methods (`trace`, `debug`, `info`, `warn`, `error`, `fatal`). The logger automatically structures output as JSON in production and redacts sensitive information.

## Errors

Throw specific errors from `src/core/error/BaseError.ts` (e.g., `ValidationError`, `PermissionError`). The global `ErrorHandler` will catch these, log them appropriately, and send safe user-facing responses.

## Commands

All commands must be Slash Commands. Do not use legacy prefix commands. Create command classes implementing `ICommand` and use `SlashCommandBuilder` from `discord.js`.

## Code Style

- Run `pnpm lint` and `pnpm format` before committing.
- Use `import ... from '...js'` extensions for ESM compatibility.
- Ensure strict TypeScript compliance (`no-any`).

## Branching & Commits

- Prefix commits with their type (e.g., `feat(tickets): add support categories`).
- Branch off `develop` and submit Pull Requests against `develop`.
