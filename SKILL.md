---
name: fui-module-development
description: Develop and publish web modules using FUI Framework. Use this skill when (1) creating new FUI modules with controls.json, (2) editing existing FUI module UI or logic, (3) publishing modules to FUI server, (4) working with FUI components like f-table or f-dialog, or (5) debugging FUI action errors.
---

# FUI Module Development

Develop web modules using FUI's metadata-driven approach where UI and logic are defined in JSON.

## Module Structure

```
<module-name>/
├── controls.json      (Core: data, watch, controls, set)
├── script.js          (Helper functions)
├── module.config.json (Framework version)
├── components/        (Custom .vue components)
└── styles/            (CSS)
```

## controls.json Anatomy

The core file has four sections:
-   **`data`**: Reactive state and named Actions
-   **`watch`**: Observers triggering actions on change
-   **`controls`**: UI layout (containers > rows > cols > elements)
-   **`set`**: Module settings (title, menu)

## Action Protocol

Define logic in `data` as named action objects. Execute with `CALL`.

| Key | Description |
|:---|:---|
| `API` | Endpoint to call |
| `IN` | Input params (use `vueData.` or `item.` refs) |
| `OUT` | Store response (e.g., `"myList"`) |
| `CALLBACK` | Action after success |
| `CONFIRM` | Show confirmation first |
| `MESS` | Toast message |
| `CALL` | Execute another named action |
| `IF/THEN/ELSE` | Conditional logic |
| `EXE` | Raw JS (use sparingly) |

**Example:**
```json
"fetchUsers": {
  "API": "/api/users",
  "IN": { "GroupID": "vueData.selectedGroup" },
  "OUT": "userList",
  "CALLBACK": { "MESS": "Loaded!" }
}
```

## Layout System (Grid & Controls)

**CRITICAL RULE**: The `controls` array MUST follow the **Mandatory Grid System** structure at the top level.

### 1. Mandatory Grid Wrapper
All controls must be wrapped in a container > rows > cols structure:
```json
"controls": [
  {
    "prop": "fluid grid-list-md",
    "rows": [
      {
        "prop": "row",
        "cols": [
          // Control Objects go here
        ]
      }
    ]
  }
]
```

### 2. Control Object Structure
Inside the `cols` array (or nested `innerHTML`), every item is a **Control Object**:

| Key | Type | Description |
|:---|:---|:---|
| **`el`** | String | HTML tag (`div`, `span`), Vue component, or FUI component. |
| **`attr`** | Object | Attributes/directives (`class`, `style`, `v-model`, `v-on:click`). **NO `@`**. |
| **`w`** | Number/String | Column width. `1-12` (grid) or `pixel value`. REQUIRED for items in `cols`. |
| **`col`** | Object | Wrapper config. Attributes for the grid column (`class`, `style`). |
| **`innerHTML`** | String/Array | Content. Can be recursive array of Control Objects. |

**Example:**
```json
{
  "el": "v-btn",
  "w": 6,
  "col": { "class": "text-center" },
  "attr": {
    "color": "primary",
    "v-on:click": "CALL(vueData.submit)"
  },
  "innerHTML": "Submit"
}
```

## Layout Rules

-   **Wrapper**: ALWAYS start with the Grid Wrapper.
-   **No `children`**: Use `innerHTML` (array) for nesting.
-   **Attributes**: Use `attr` for element attributes. Use `col` for grid column attributes.
-   **Events**: Use `v-on:click` (valid JSON), not `@click`.


## MCP Tools

Use these tools to interact with FUI:

-   **`save_module`**: Download module from server → `projectId`, `moduleId`, `outputDir`
-   **`publish_module`**: Upload module to server → `projectId`, `moduleId`, `moduleDir`
-   **`publish_component`**: Upload a `.vue` component → `projectId`, `moduleId`, `componentName`, `componentPath`

## UI Templates

Copy templates from `examples/` as starting points. See [ui-templates.md](references/ui-templates.md) for usage guide.

| Template | Type | Use Case |
|:---|:---|:---|
| [form-basic.json](examples/form-basic.json) | JSON | Simple input forms |
| [table-crud.json](examples/table-crud.json) | JSON | Data tables with CRUD |
| [dialog-form.json](examples/dialog-form.json) | JSON | Modal dialogs |
| [component.vue](examples/component.vue) | Vue | Custom component starter |

## Instructions

1.  **Creating New Modules**: ALWAYS create a ROOT DIRECTORY with the module name first (e.g., `my-module/`). ALl files (`controls.json`, `script.js`, etc.) MUST be inside this directory.
    -   `controls.json` (Required): Define UI and Logic.
    -   `module.config.json` (Required): Framework config.
    -   `styles/index.css` (Optional): Custom CSS (No `<style>` in .vue).
    -   `components/` (Optional): Custom Vue components.

2.  **Reference Docs**: See `references/` for component and function details:
    -   [fastproject.md](references/fastproject.md) - Core action engine
    -   [default-function.md](references/default-function.md) - Utility functions
    -   [coding-standards.md](references/coding-standards.md) - Class naming & Menu config
    -   [controls-patterns.md](references/controls-patterns.md) - Action patterns & Logic
    -   [ui-templates.md](references/ui-templates.md) - Template usage guide

3.  **Editing controls.json**: Use valid JSON. Reference state with `vueData.` prefix.

4.  **UI Templates**: Copy from `examples/`, modify APIs and fields.