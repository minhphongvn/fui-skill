# FUI Coding Standards

## 1. Naming Conventions

### Components (`components/`)
-   **Prefix**: Use `uc-` (User Component) for custom module components to distinguish from standard FUI components (`f-`, `t-`).
-   **Format**: Kebab-case (e.g., `uc-trangthai-sukien.vue`, `uc-user-profile.vue`).
-   **Props**: Use camelCase in script, kebab-case in templates (e.g., `userProfile` -> `:user-profile`).

### CSS Classes
-   **No `<style>` Tags**: Do not use `<style>` in `.vue` files. All custom styles must go in `styles/index.css`.
-   **Vuetify Utilities**: Prioritize Vuetify helper classes (e.g., `ma-2`, `pa-0`, `d-flex`, `primary--text`).
-   **Custom Classes**: Use meaningful names, avoid generic names like `.box` or `.red`.
-   **State Classes**: Use descriptive names for state (e.g., `.is-active`, `.has-error`).

### Action Keys (`controls.json`)
-   **API Actions**: Predix with `api` (e.g., `apiGetDSSuKien`, `apiUpdateUser`).
-   **Event Handlers**: Prefix with `handle` (e.g., `handleOpenReport`, `handleSubmit`).
-   **Dialog Actions**: Prefix with verb (e.g., `openUploadDialog`, `closeSettings`).

## 2. Menu Configuration (`set.menu`)

Define the application menu in the `set` object of `controls.json`.

```json
"menu": [
  {
    "name": "Main Group",
    "icon": "mdi-home",    // Material Design Icons
    "url": "/dashboard",   // Route
    "right": {             // Permission check
      "SystemRight": [1, 2] // Array of allowed Right IDs
    }
  },
  {
    "name": "Management",
    "icon": "mdi-cog",
    "submenu": [           // Nested menu items
      {
        "name": "Users",
        "url": "/users"
      },
      {
        "name": "Settings",
        "url": "/settings"
      }
    ]
  }
]
```

## 3. Project Structure

-   **`components/`**: Only place `.vue` files here. Do not sub-folder unless strictly necessary (FUI auto-scans this root).
-   **`styles/`**: Custom CSS files. Ensure `index.css` is the entry point if multiple files exist.
-   **`controls.json`**: Keep this file clean. Move large static lists to the database or separate JSON files if supported.

## 4. Best Practices

-   **Data Binding**: Avoid complex logic in JSON attributes. Use computed properties in components or simpler `vueData` structures.
-   **Event Handling**: Use `CALL(vueData.actionName)` for all complex interactions. Avoid inline JS like `vueData.count++` for anything beyond simple toggles.
-   **Mobile Responsiveness**: Always configure `configForm.xs` and `configForm.md` for responsive form widths.
