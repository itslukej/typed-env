# typed-env

[![npm version](https://img.shields.io/npm/v/typed-env.svg?maxAge=3600)](https://npmjs.com/package/typed-env)
[![monthly downloads](https://img.shields.io/npm/dm/typed-env.svg?maxAge=3600)](https://npmjs.com/package/typed-env)

A typed environment variable parser with support for choices, custom parsers, and more.

## Usage

```ts
import { createEnv } from 'typed-env';

const env = createEnv({
  PORT: { type: 'number', default: 80 }
});

env.PORT; // number
```

## Features

- Strongly typed
- Supports [custom parsers](#parser)
- Supports optional environment variables
- Supports limiting the possible values (see [Choices](#choices))
- Supports passing custom environments (see [Options](#options))

### Choices

```ts
import { createEnv } from 'typed-env';

const env = createEnv({
  NODE_ENV: {
    type: 'string',
    choices: ['development', 'production']
  }
});

env.NODE_ENV; // 'development' | 'production'
```

### Parser

You can pass a `parser` function to return your own custom type

```ts
import { createEnv } from 'typed-env';

const env = createEnv({
  HOMEPAGE: { parser: url => new URL(url) }
});

env.HOMEPAGE; // URL
```

### Options

If you want to use a custom env, pass `env` in the `options` parameter, otherwise it will load from `process.env`

```ts
interface Options {
  env?: Record<string, string> | NodeJS.ProcessEnv;
}
```
