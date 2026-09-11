# MAUI Designer

An independent fork of [GMPrakhar's MAUI-Designer](https://github.com/GMPrakhar/MAUI-Designer),
maintained by [hiadamhere](https://github.com/hiadamhere). We are building our own
direction on the foundation created by GMPrakhar and the upstream contributors.
The inherited implementation and capabilities described below are our starting
point; they are not presented as new work by this fork.

The repository includes an Angular web designer, a Windows-native MAUI designer,
and a Visual Studio extension. See the [native app guide](maui-designer-native/README.md)
and [extension guide](extension/README.md) for their setup and validation steps.
The feature and usage sections below describe the web designer.

**Upstream web demo:** [GMPrakhar's hosted designer](https://gmprakhar.github.io/MAUI-Designer/).
This is the upstream deployment and does not represent changes made in this fork.

Development is integrated on `develop`. Changes are promoted to `main` through
an explicitly approved pull request, and release tags are created only after
that merge. See [CONTRIBUTING.md](CONTRIBUTING.md).

> The web app is a **MAUI XAML-aware HTML/CSS designer**. It does not run the MAUI
> renderers, so the canvas is an approximation. The Windows-native app in
> [`maui-designer-native/`](maui-designer-native/README.md) hosts **real MAUI views**
> on WinUI. [DevFlow](docs/maui-labs.md) (from maui-labs) inspects that live tree; it
> is not a designer itself.

![MAUI Designer](https://img.shields.io/badge/Angular-18.2.0-red) ![TypeScript](https://img.shields.io/badge/TypeScript-5.5.4-blue) ![License](https://img.shields.io/badge/License-GPLv3-blue)

## 🚀 Features

### Visual Design Tools
- **Drag-and-Drop Interface**: Intuitive visual design with drag-and-drop functionality
- **Element Toolbox**: Comprehensive collection of MAUI controls and layouts
- **Properties Panel**: Real-time property editing with immediate visual feedback
- **Hierarchy Panel**: Tree view of element structure for easy navigation
- **Resizable Panels**: Customizable workspace with adjustable panel sizes
- **Toolbox Search**: Filter the control list as you type
- **Undo/Redo**: Full history for every design change (`Ctrl+Z` / `Ctrl+Y`)
- **Keyboard Shortcuts**: `Delete` to remove, `Ctrl+D` to duplicate, arrow keys to nudge, `Esc` to deselect
- **Layout Alignment**: `HorizontalOptions` and `VerticalOptions` on every control
- **Lossless XAML Round Trip**: Attributes the designer does not model are preserved instead of dropped
- **Local Persistence**: Save and restore your design in the browser

### Multi-Selection
- **Shift/Ctrl+Click**: Add or remove elements from the selection
- **Marquee Selection**: Rubber-band across the canvas to grab everything it touches
- **Select All**: `Ctrl+A` selects every child of the current layout
- **Bulk Editing**: Shared width, height, background colour and visibility in the properties panel
- **Bulk Actions**: Delete, duplicate, nudge and align a whole selection in one undo step

### Alignment & Layout Tools
- **Align**: Left, centre, right, top, middle and bottom for any multi-selection
- **Distribute**: Even horizontal or vertical spacing for three or more elements
- **Snap to Grid**: Configurable grid size with snapping while dragging
- **Smart Guides**: Live guides when a dragged element lines up with a sibling or the page edges/centre
- **Rulers**: Optional horizontal and vertical rulers around the design surface
- **Theming**: Per-property light/dark colours emitted as `AppThemeBinding`, previewed against the toolbar theme
- **Accessibility**: `SemanticProperties` editing plus live WCAG AA contrast checking
- **Z-Order**: Bring to front, send to back and single-step restacking (`Ctrl+]` / `Ctrl+[`, add `Shift` to jump to either end)

### Clipboard, Templates & Starter Pages
- **Copy/Cut/Paste**: `Ctrl+C`, `Ctrl+X`, `Ctrl+V` (containers keep their children, names stay unique)
- **Component Templates**: Save any selection as a reusable template, stored in the browser
- **Starter Pages**: Login, list, profile and settings pages ready to drop onto the canvas

### Live Preview
- **Device Presets**: Phone, small phone, tablet, desktop or a custom surface size
- **Zoom & Pan**: Toolbar buttons, `Ctrl` + mouse wheel, and `Space` + drag (or middle-drag) to pan
- **Fit to Window**: One click to scale the design to the available space
- **Dark Mode Preview**: Toggle a dark canvas to check contrast
- **Persisted View**: Zoom, theme and grid settings survive a reload

### Custom Controls from NuGet Packages
- **Manifest Registry**: Describe third-party controls (Syncfusion, Telerik, DevExpress, in-house libraries) in a small JSON manifest and they appear in the toolbox, properties panel and canvas
- **Bundled CommunityToolkit.Maui Pack**: `AvatarView`, `Expander`, `DrawingView`, `MediaElement`, `Popup` and `SemanticOrderView` work out of the box
- **Import & Export**: Load manifests from disk, export the whole registry as one JSON file, remove packs you no longer need
- **Lossless Round-Trip**: Unknown vendor tags in imported XAML are preserved verbatim — namespaces, attributes, property elements and nested children all survive a parse/generate cycle
- **Learning Parser**: Controls that are not in any manifest are inferred from the XAML (including property types) and added to the toolbox automatically
- **Raw Attribute Editor**: Any attribute the manifest does not declare is still editable in the properties panel

### XAML Integration
- **XAML Editor**: Full-featured code editor with syntax support
- **Real-time Preview**: Instant visual updates when applying XAML changes
- **XAML Generation**: Export designed layouts as clean XAML code
- **XAML Parsing**: Import existing XAML files to recreate visual designs
- **Copy & Download**: Easy sharing and saving of generated XAML
- **File Import**: Load a `.xaml` file, or convert an `.svg` icon into MAUI `Path` elements
- **Grid Definitions**: Row/column definitions (`Auto`, `*`, absolute) size the canvas tracks and round-trip through XAML. `RowSpan` / `ColumnSpan` stretch the child across those tracks.

### Supported MAUI Elements

#### Controls
- **Label**: Text display with formatting options
- **Button**: Interactive buttons with styling
- **Image**: Image display with positioning
- **ProgressBar**: Determinate progress with a `Progress` value
- **ActivityIndicator**: Busy indicator with an `IsRunning` flag
- **CollectionView**: Repeating list with an editable `ItemTemplate`

#### Inputs
- **Entry**: Single-line text input with placeholder support
- **Editor**: Multi-line text input areas
- **SearchBar**: Search input with placeholder
- **CheckBox**: Two-state check box
- **Switch**: Toggle switch
- **Slider**: Minimum/maximum/value slider
- **Stepper**: Increment/decrement stepper
- **DatePicker**: Date selection

#### Layouts
- **StackLayout**: Vertical/horizontal stacking of elements
- **Grid**: Row and column-based layouts with spanning
- **AbsoluteLayout**: Precise positioning with coordinates

#### Views
- **Frame**: Containers with borders and backgrounds
- **Border**: Container with stroke, thickness and corner radius
- **ScrollView**: Scrollable content areas

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** matching the version selected in [web CI](.github/workflows/ci.yml)
- **npm** bundled with that Node.js installation
- **Angular CLI** installed locally by `npm ci`; a global installation is not required

## 📦 Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/hiadamhere/MAUI-Designer.git
   cd MAUI-Designer
   ```

2. **Install dependencies:**
   ```bash
   npm ci
   ```

## 🚀 Getting Started

### Development Server

Start the development server:

```bash
npm start
```

Navigate to `http://localhost:4200/` in your browser. The application will automatically reload when you make changes to the source files.

### Building for Production

Build the project for production:

```bash
npm run build
```

The build artifacts will be stored in the `dist/` directory.

### Running Tests

Unit tests (Karma + Jasmine):

```bash
npm test                # watch mode
npm run test:headless   # single headless run (CI friendly)
```

End-to-end tests (Playwright, headless Chromium). The Angular dev server is started
automatically on port 4300:

```bash
npx playwright install chromium   # once
npm run e2e                       # run the suite
npm run e2e:report                # open the last HTML report
```

To run the suite against an already running instance (for example a production build):

```bash
E2E_BASE_URL=http://localhost:4400 npm run e2e
```

The specs live in `e2e/` and cover the shell, toolbox, canvas, hierarchy, properties
panel, grid editing, undo/redo, persistence and the XAML editor.

### Deploying to GitHub Pages

The app is fully client side, so it can be hosted as a static site. Pushing to `main`
runs `.github/workflows/deploy-pages.yml`, which builds with the correct base href,
adds an SPA `404.html` fallback and publishes to GitHub Pages.

Enable it once via **Settings → Pages → Build and deployment → Source: GitHub Actions**.

Build the same bundle locally with:

```bash
npm run build:pages
```

## 🎯 Usage Guide

### 1. Creating Your First Layout

1. **Select a Layout Container**: Start by adding a layout container (StackLayout, Grid, or AbsoluteLayout) from the toolbox
2. **Add Controls**: Drag controls like Label, Button, or Entry from the toolbox to your layout
3. **Configure Properties**: Use the Properties panel to customize appearance, text, colors, and positioning
4. **Preview XAML**: Check the XAML tab to see the generated code in real-time

### 2. Working with the Toolbox

The toolbox is organized into three categories:

- **Controls**: Interactive elements like buttons, labels, and input fields
- **Layouts**: Containers that organize child elements (StackLayout, Grid, AbsoluteLayout)
- **Views**: Specialized containers like Frame and ScrollView

### 3. Properties Panel

The Properties panel allows you to modify:

- **Layout Properties**: Position (x, y), size (width, height), margins, padding
- **Visual Properties**: Background color, text color, font family, font size
- **Content Properties**: Text content, images, and other element-specific properties
- **Grid Properties**: Row/column position and spanning for Grid layouts
- **Control Properties**: Placeholder, checked/toggled state, slider range, progress, corner radius, and more
- **Data Bindings**: Bind any supported property to a view-model path; the generated XAML emits `{Binding Path}` instead of the literal value

### 4. XAML Editor

- **Apply Changes**: Click the "Apply" button to update the visual design from XAML code
- **Reset**: Revert to the current visual design state
- **Copy**: Copy the generated XAML to clipboard
- **Download**: Save the XAML as a file

### 5. Hierarchy Panel

- View the complete element structure
- Select elements for editing
- Navigate complex layouts easily

### 6. Custom Controls from NuGet Packages

The designer does not need to reference your NuGet package — it only needs a description of the
controls. Drop a JSON manifest into **Toolbox → Custom controls → Import**:

```json
{
  "id": "syncfusion-inputs",
  "package": "Syncfusion.Maui.Inputs",
  "xmlns": {
    "prefix": "sf",
    "uri": "clr-namespace:Syncfusion.Maui.Inputs;assembly=Syncfusion.Maui.Inputs"
  },
  "controls": [
    {
      "tag": "SfComboBox",
      "displayName": "Combo box",
      "icon": "arrow_drop_down_circle",
      "defaultWidth": 200,
      "defaultHeight": 40,
      "isContainer": false,
      "preview": { "kind": "box", "label": "{Placeholder}" },
      "properties": [
        { "name": "Placeholder", "type": "string", "defaultValue": "Select an item" },
        { "name": "IsEditable", "type": "boolean", "defaultValue": false },
        { "name": "MaxDropDownHeight", "type": "number", "defaultValue": 200 }
      ]
    }
  ]
}
```

Manifest reference:

| Field | Meaning |
| --- | --- |
| `id` | Stable identifier used for updates and removal |
| `package` | NuGet package name, shown in the toolbox and properties panel |
| `xmlns.prefix` / `xmlns.uri` | XML namespace emitted in the generated XAML |
| `controls[].tag` | The XAML tag, e.g. `SfComboBox` |
| `controls[].isContainer` | `true` if the control accepts child elements |
| `controls[].preview` | Canvas rendering: `kind` of `box`, `text`, `image`, `list` or `slot`, plus `label`, `backgroundColor`, `textColor`, `borderColor`, `cornerRadius`, `icon` |
| `controls[].properties[]` | Editable properties: `name`, `type` (`string`, `number`, `boolean`, `color`, `enum`), `defaultValue`, `options`, `bindable` |

`{Property}` placeholders inside `preview.label` and the colour fields are interpolated from the
element's current values, so the canvas preview updates as you edit.

Registered manifests are stored in `localStorage` under `maui-designer.custom-controls`. The
namespace URI is also stored on each element, so pasted XAML keeps working even if the manifest is
removed later.

## 🏗️ Project Structure

```
src/
├── app/
│   ├── components/           # UI Components
│   │   ├── designer-canvas/  # Main design surface
│   │   ├── hierarchy-panel/  # Element tree view
│   │   ├── properties-panel/ # Property editor
│   │   ├── toolbox/         # Element toolbox
│   │   └── xaml-editor/     # XAML code editor
│   ├── models/              # Data models
│   │   ├── maui-element.ts  # MAUI element definitions
│   │   └── toolbox.ts       # Toolbox item definitions
│   ├── services/            # Business logic services
│   │   ├── drag-drop.ts     # Drag-and-drop functionality
│   │   ├── element.ts       # Element management
│   │   ├── layout-designer.ts # Layout calculations
│   │   ├── xaml-generator.ts # XAML code generation
│   │   └── xaml-parser.ts   # XAML parsing
│   └── app.ts              # Main app component
├── styles.scss             # Global styles
└── index.html             # Main HTML file

e2e/                        # Playwright end-to-end tests
├── helpers/designer-page.ts # Page object with data-testid locators
├── app-shell.spec.ts
├── toolbox.spec.ts
├── canvas.spec.ts
├── hierarchy-panel.spec.ts
├── properties-panel.spec.ts
├── undo-redo.spec.ts
├── persistence.spec.ts
└── xaml-editor.spec.ts
```

> UI elements expose `data-testid` attributes for the e2e suite. Keep them stable when
> refactoring templates.

## 🔧 Development

### Architecture

The application follows Angular's standalone components architecture with a service-based approach:

- **Components**: Each UI panel is a standalone component with its own logic
- **Services**: Business logic is centralized in injectable services
- **Models**: TypeScript interfaces define data structures for MAUI elements
- **Reactive Programming**: Uses RxJS for state management and real-time updates

### Key Services

- **ElementService**: Manages element creation, selection, and hierarchy
- **LayoutDesignerService**: Handles layout calculations and positioning
- **XamlGeneratorService**: Converts visual designs to XAML code
- **XamlParserService**: Parses XAML code into visual elements
- **DragDropService**: Manages drag-and-drop interactions
- **AlignmentService**: Aligns, distributes, snaps and computes smart guides
- **ViewportService**: Zoom, pan, device preset, theme and grid settings (persisted)
- **ClipboardService**: Copy/cut/paste, component templates and starter pages

### Adding New MAUI Elements

1. **Define the element type** in `models/maui-element.ts`
2. **Add toolbox entry** in `models/toolbox.ts`
3. **Implement element creation** in `services/element.ts`
4. **Add XAML generation logic** in `services/xaml-generator.ts`
5. **Update parser** in `services/xaml-parser.ts`

## 🤝 Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) for the branch flow, local review process,
and validation commands. [AGENTS.md](AGENTS.md) defines the shared engineering
standards for agent-assisted contributions. Contributions to this fork target
`hiadamhere/MAUI-Designer`.

## 📋 Technology Stack

- **Frontend Framework**: Angular 18.2.0
- **UI Components**: Angular Material 18.2.0
- **Drag & Drop**: Angular CDK 18.2.0
- **Language**: TypeScript 5.5.4
- **Styling**: SCSS
- **State Management**: RxJS 7.8.0
- **Build Tool**: Angular CLI 18.2.0
- **Testing**: Jasmine & Karma

## 🐛 Known Issues

- Build may fail in environments without internet access due to Google Fonts dependency
- Some advanced XAML features are not yet supported
- Complex nested layouts may require manual XAML adjustments

## 🧩 IDE Integration

The designer also runs **inside Visual Studio 2022**. [`extension/`](extension/README.md) contains a
VSIX that registers the designer as an alternative editor for `.xaml` files: it edits the same text
buffer as the built-in XAML editor (so undo, the dirty marker and Ctrl+S all behave normally), and it
generates toolbox entries from the controls in the project's own NuGet packages by inspecting
`obj/project.assets.json` and the package assemblies.

### Installing the extension (beta)

> **Beta — expect it to break.** The extension is new and has had far less real-world use than the
> web app. It may misbehave or fail outright; don't rely on it for important work, and keep your
> XAML in source control.

The [upstream beta download][vsix-download] is published by GMPrakhar; it does
not contain this fork's changes. To build this fork, follow the
[extension build instructions](extension/README.md). To try the upstream binary:

1. Close Visual Studio.
2. Double-click the downloaded `.vsix` and complete the VSIX installer.
3. Reopen Visual Studio, right-click a `.xaml` page and choose **Open With… → MAUI Designer**.

Requires Windows, Visual Studio 2022 or 2026 (17.0 or later) and the WebView2 runtime (already present on
current Windows installs). To uninstall, use **Extensions → Manage Extensions**.

[vsix-download]: https://github.com/GMPrakhar/MAUI-Designer/releases/download/vsix-latest/MauiDesigner.vsix

- [`extension/README.md`](extension/README.md) — how to build, test and debug the VSIX
- [`docs/visual-studio-extension.md`](docs/visual-studio-extension.md) — the design rationale, and
  why the classic in-process VSSDK model is required

The web app detects its host at runtime (`src/app/services/host-bridge.ts`). In a plain browser
nothing changes; inside an IDE the open document becomes the source of truth instead of browser
storage.

## 📚 Resources

- [MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/)
- [Angular Documentation](https://angular.io/docs)
- [Angular Material](https://material.angular.io/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)

## 📄 License

Licensed under the [GNU General Public License v3.0](LICENSE.md) only.

You may use, study, share and modify this software, including commercially,
as long as derivative works are also distributed under GPL-3.0 and you provide
the corresponding source. See the licence for the full terms.

Earlier revisions of this README stated MIT, then PolyForm Noncommercial;
nothing here retroactively withdraws rights anyone already relied on under
those statements.

The dependencies keep their own licences (Angular and the rest are MIT); this
applies only to the code in this repository.

## 👨‍💻 Attribution and maintenance

- **Original project:** [GMPrakhar](https://github.com/GMPrakhar) and the
  contributors to [GMPrakhar/MAUI-Designer](https://github.com/GMPrakhar/MAUI-Designer).
- **This independent fork:** [hiadamhere/MAUI-Designer](https://github.com/hiadamhere/MAUI-Designer),
  maintained by [hiadamhere](https://github.com/hiadamhere).

This fork retains the upstream Git history and license. Its direction and changes
are maintained independently; upstream authorship is preserved and acknowledged.

## 🙏 Acknowledgments

- Microsoft MAUI team for the excellent UI framework
- Angular team for the robust web framework
- Contributors and community members

---

**Happy Designing!** 🎨
