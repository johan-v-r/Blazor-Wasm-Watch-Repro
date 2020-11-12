# Blazor-Wasm-Watch-Repro

This repo serves as an example to reproduce the following `dotnet watch` issues:

1. Exclude/Remove watched files (configured in `csproj`) not honored.
1. Saving `scss` files in different folders cause the watch to loop infinitely.

These issues were picked up in a different (work) project, and this is the simplest & closest solution to replicate from a _File -> New_ scaffold.

___

## Steps to replicate:

1. `cd src\BlazorAppWatch`
1. `dotnet build`
1. `dotnet watch run`
1. Save the `src\BlazorAppWatch\Shared\MainLayout.razor.scss` file (any editor will do).

This results in:

```powershell
PS C:\SourceCode\Blazor-Wasm-Watch-Repro\src\BlazorAppWatch> dotnet watch run
watch : Started
Building...
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:5000
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: C:\SourceCode\Blazor-Wasm-Watch-Repro\src\BlazorAppWatch

watch : Exited
watch : File changed: C:\SourceCode\Blazor-Wasm-Watch-Repro\src\BlazorAppWatch\Shared\MainLayout.razor.scss
watch : Started
Building...

watch : Exited
watch : File changed: C:\SourceCode\Blazor-Wasm-Watch-Repro\src\BlazorAppWatch\Pages\Counter.razor.css
watch : Started
Building...

watch : Exited
watch : File changed: C:\SourceCode\Blazor-Wasm-Watch-Repro\src\BlazorAppWatch\Pages\Counter.razor.css
watch : Started
Building...
watch : Shutdown requested. Press Ctrl+C again to force exit.

The build failed. Fix the build errors and run again.

watch : Exited
```