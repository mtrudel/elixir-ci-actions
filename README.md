# GitHub Actions for Elixir CI

This repo contains a number of basic workflows for testing and linting Elixir
projects, encapsulating best practices around artifact caching & linting. 

To use these workflows, you can create a `.github/workflows/elixir.yml` (or similar named)
file in your repository with the following content:

```yaml
name: Elixir CI

on:
  push:
    branches: [ main ]
  pull_request:
  workflow_dispatch:

jobs:
  test:
    uses: mtrudel/elixir-ci-actions/.github/workflows/test.yml@main
  lint:
    uses: mtrudel/elixir-ci-actions/.github/workflows/lint.yml@main
```

For examples of projects which use these workflows, you can look at
[Bandit](https://github.com/mtrudel/bandit), [Thousand
Island](https://github.com/mtrudel/thousand_island), or
[HAP](https://github.com/mtrudel/hap), among others.

## The `test` workflow

The `test` workflow does the following:
  * Compiles your dependencies, ignoring any warnings
  * Compiles your project code with `--warnings-as-errors`
  * Runs `mix test`

The `test` workflow runs in a matrix of the three latest major Elixir and Erlang
releases, using the latest minor/patch version of each. Combinations which are
not supported are automatically excluded from the matrix.

## The `lint` workflow

The `lint` workflow does the following:
  * Compiles your dependencies, ignoring any warnings
  * Compiles your project code with `--warnings-as-errors`
  * Runs `mix format --check-formatted`
  * Runs `mix credo --strict`
  * Runs `mix dialyzer`

The `lint` workflow runs in the latest major Elixir and Erlang
releases, using the latest minor/patch version of each. 

## License

MIT
