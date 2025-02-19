[![License: MIT](https://img.shields.io/badge/license-MIT-purple.svg)](https://opensource.org/licenses/MIT)
[![Coverage](https://codecov.io/gh/our-creativity/disco/graph/badge.svg?token=Z19R32RJ22)](https://codecov.io/gh/our-creativity/disco)
[![GitHub issues](https://img.shields.io/github/issues/our-creativity/disco)](https://github.com/our-creativity/disco/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/our-creativity/disco.svg)](https://gitHub.com/our-creativity/disco/pull/)
[![pub.dev Version (including pre-releases)](https://img.shields.io/pub/v/disco?include_prereleases)](https://pub.dev/packages/disco)
[![GitHub stars](https://img.shields.io/github/stars/our-creativity/disco)](https://gitHub.com/our-creativity/disco/stargazers/)

# Disco

A modern, convenient, simple and safe way to do scoped dependency injection in Flutter.

For learning how to use [Disco](https://github.com/our-creativity/disco), see its documentation: >>> https://disco.mariuti.com <<<

## Features

- Scoped dependency injection
- Service locator
- Testable
- Independent of state management solutions
  - This library focuses on DI, so that state management solutions can focus on the reactivity.

## Usage

1. Create a provider

    ```dart
    final modelProvider = Provider((context) => Model());
    ```

2. Scope/provide the provider

    ```dart
    ProviderScope(
      providers: [modelProvider],
      child: MyWidget(),
    )
    ```

3. Inject the provider (within the above `ProviderScope`'s subtree)

    ```dart
    final model = modelProvider.of(context);
    ```

## Examples

There are multiple examples on the repository:

- [basic](https://disco.mariuti.com/examples/basic/) A basic example showing the basic usage of Disco.
- [solidart](https://disco.mariuti.com/examples/solidart/) An example showcasing the power of the `ProviderScope` widgets combined with solidart reactivity.
- [bloc](https://disco.mariuti.com/examples/bloc/) An example showcasing how to provide a light/dark theme Cubit with Disco.
- [auto_route](https://disco.mariuti.com/examples/auto-route/) An example showing how to share a provider between multiple pages without scoping the entire app.
- [preferences](https://disco.mariuti.com/examples/preferences/) An example showing how to provide async objects with Disco.

## Additional information

This library can be used in combination with many existing packages.

### State management

This package is not opinionated about reactivity: feel free to use your
state management solution of choice (as long as it is compatible with the
concepts of the library).

#### Compatible solutions

Compatible state management solutions are those whose signals/observables can be created locally and passed as arguments, such as
- [`solidart`](https://pub.dev/packages/flutter_solidart) (NB: its providers up to
version `2.0.0-dev.2` will be replaced with the ones present in `disco`),
- `ValueNotifier`/`ChangeNotifier` (from Flutter)
- [`bloc`](https://pub.dev/packages/flutter_bloc) (NB: the usage of `BlocProvider` should be replaced with the providers present in this library).

Our repository includes one example with `solidart` and one with `bloc`.

#### Incompatible solutions

State management solution entirely leveraging global state, such as [`riverpod`](https://pub.dev/packages/riverpod), are not compatible with this library.

### Contributions

The purpose of this package is to simplify dependency injection for everyone.
PRs are welcome, especially for documentation and more examples. Another goal of this library is to be simple. PRs introducing new features or breaking changes will have to be explained in detail.
