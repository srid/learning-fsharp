[Introduction to ASP.NET Core Blazor](https://docs.microsoft.com/en-ca/aspnet/core/blazor/?view=aspnetcore-5.0) gives a thorough technical overview.

## WebAssembly vs Server

Two notions worthy of note in Blazor are

- [Blazor WebAssembly](https://docs.microsoft.com/en-ca/aspnet/core/blazor/?view=aspnetcore-5.0#blazor-webassembly)
- [Blazor Server](https://docs.microsoft.com/en-ca/aspnet/core/blazor/?view=aspnetcore-5.0#blazor-server)

The former makes the client app effectively a SPA (running in the browser) -- this is how traditional JavaScript client apps work.

![Blazor WebAssembly runs .NET code in the browser with WebAssembly.](https://docs.microsoft.com/en-ca/aspnet/core/blazor/index/_static/blazor-webassembly.png?view=aspnetcore-5.0)

However the later, Blazor Server, is more interesting, because that makes the "client" app *mostly run on the server*. 

"mostly" - because, when dealing with UI events from DOM as well as when modifying the DOM itself, Blazor communicates over the wire (through [[SignalR]]) to the frontend browser. Otherwise the rest of the code logic runs on the server.

![Blazor Server runs .NET code on the server and interacts with the Document Object Model on the client over a SignalR connection](https://docs.microsoft.com/en-ca/aspnet/core/blazor/index/_static/blazor-server.png?view=aspnetcore-5.0)