# Blazor in .NET 8 RC2

Please read the documentation at https://devblogs.microsoft.com/dotnet/asp-net-core-updates-in-dotnet-8-rc-2/#blazor

These are the topics I cover in [BlazorTrain](https://blazortrain.com/) episode 99:

### Global interactivity for Blazor Web Apps

The Blazor Web App template has new options to enable an interactive render mode for the entire app instead of just for individual pages. Enabling an interactive render mode globally means the entire app becomes interactive including the router and layout. Page navigations benefit from client-side routing and every page can use interactive features. This option is very similar in functionality to how existing Blazor Server and Blazor WebAssembly apps function.

### Combining Server-Side Rendering with Streaming Rendering

I modified the *Weather.razor* page to output SSR rendered HTML before the streaming output by calling `StateHasChanged()` in the `OnInitializedAsync()` method after setting a string to show in the UI, and before pausing for the streaming data.

### File scoped `@rendermode` Razor directive

The `@rendermode` Razor directive can now be applied at the file scope to specify a render mode on a component definition instead of using the existing render mode attributes.

The `@rendermode` directive takes a single parameter of type `IComponentRenderMode`, just like it does when used as a Razor directive attribute on a component instance. The `RenderMode` static class provides convenience properties for the currently supported render modes: `InteractiveServer`, `InteractiveWebAssembly`, and `InteractiveAuto`. You can use a `using static` directive in your *_Imports.razor* file to simplify access to these render mode properties.

### Enhanced navigation & form handling improvements

Blazor in .NET 8 enhances navigation and form handling by intercepting the requests and intelligently updating the DOM with the statically rendered content from the server. In this release, we’ve made some improvements to how enhanced navigation & form handling works so that you have more control over when the enhancements are applied and so the enhancements integrate well with other non-Blazor pages.

### Close circuits when there are no remaining interactive server components

Interactive server components handle web UI events using a real-time connection with the browser called a circuit. A circuit and its associated state are setup when a root interactive server component is rendered. In .NET 8 RC2, the circuit will now be closed when there are no remaining interactive server components on the page, which frees up server resources.