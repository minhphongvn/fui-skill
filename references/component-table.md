# FUI Component Table System

This document references the table components and cell renderers defined in `componentTable.js`.

## Table Components

### f-table
A feature-rich data table with support for CRUD operations, search, and export.

**Props:**
- `value`: Array of items or selected items (v-model).
- `headers`: Array of column definitions.
- `items`: Data array.
- `label`: Table title/label.
- `itemKey`: Unique key for items (default: `id` or specified).
- `showSearch`: Boolean to enable search bar.
- `excel`: Boolean to enable Excel export button.
- `updateApi`: Object defining API endpoints for CRUD (`new`, `edit`, `delete`, `default-item`, `data-out`).
- `updateForm`: JSON configuration for the Add/Edit dialog form.
- `updateFormAttr`: Attributes for the Add/Edit dialog.
- `disabledUpdate`: Boolean to disable Add/Edit/Delete actions.
- `sumFormat`: Format string for summary footer (e.g., `Total: [[amount]]`).

**Behavior:**
- **CRUD**: Automatically handles displaying a dialog for creating/editing items if `updateApi` and `updateForm` are provided.
- **Selection**: Supports row selection if `v-model` is bound.

### f-table-view
A simplified, read-only version of `f-table` (or with limited interactivity).

**Props:**
- `items`: Data array.
- `headers`: Column definitions.
- `label`: Table label.
- `showSearch`: Enable search.
- `excel`: Enable Excel export.

## Cell Renderers (t-*)
These components are used within `f-table` or `f-table-view` cells to format specific data types.

### t-label
Displays simple text.
- **Props:** `value` (Text to display).

### t-html
Displays data as HTML.
- **Props:** `value` (HTML string).

### t-num
Formats numbers.
- **Props:**
  - `value`: Number.
  - `format`: Numeral.js format string (default handles integers vs floats).
  - `hidezero`: Boolean to hide zero values.

### t-time
Formats date/time.
- **Props:**
  - `value`: Date/Time string.
  - `format`: Moment.js format string (default: `DD/MM/YYYY`).

### t-boolean
Displays a boolean as an icon (Check/Close).
- **Props:**
  - `value`: Boolean.
  - `colorTrue`, `colorFalse`: Colors for icons.
  - `iconTrue`, `iconFalse`: Icon names.

### t-check
Renders a checkbox (editable in table).
- **Props:** `value`.
- **Event:** Triggers `action` on change.

### t-text
Renders a text input (editable in table).
- **Props:** `value`.

### t-select
Renders a dropdown select (editable in table).

### t-combobox
Renders an autocomplete combobox (editable in table).
- **Props:**
  - `api`: API endpoint to fetch items.
  - `items`: Static items array.

### t-menu
Renders a dropdown menu icon.
- **Props:**
  - `items`: Menu items.
  - `iconText`: Icon for the menu button.

### t-link
Renders a clickable link.
- **Props:**
  - `url`: Target URL.
  - `target`: `_blank`, `dialog`, etc.

### t-button
Renders an action button.
- **Props:**
  - `label`: Button text.
  - `action`: Action to perform on click.