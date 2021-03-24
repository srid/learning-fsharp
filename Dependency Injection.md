---
slug: DI
---

Dependency Injection relates to things like Reader monad and Free monad from [[Haskell]]-like languages.

If you are familiar with Haskell a quick read through [# Six approaches to dependency injection](https://fsharpforfunandprofit.com/posts/dependencies/) is useful.

Then, from a practical standpoint of view, DI is used in `Startup.fs` (or `Startup.cs`) to inject service dependencies. For example, in [[fsharp-wasm-static-demo]] we inject the `HttpClient` dependency in `Startup.fs` and that is automatically made available in `Program.fs`.
