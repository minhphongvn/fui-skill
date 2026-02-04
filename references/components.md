# FUI Components

This document references the general UI components defined in `component.js`.

## Input & Display Components

### f-qrcode-reader
A component for reading QR codes (functionality implies reading/displaying).
- **Props:**
  - `value`: Input value.
  - `size`: Size of the QR code.
  - `logo`: Logo image to embed.

### f-image-update
A component for displaying and updating images.
- **Props:**
  - `src`: Image source URL.
  - `size`: Display size.
  - `view`: View mode.
  - `editable`: Boolean to enable upload/edit.

### f-date
A wrapper for a date picker.
- **Props:**
  - `value`: Date string.
  - `label`: Field label.
  - `icon`: Custom icon.

### f-time
A wrapper for a time picker.
- **Props:**
  - `value`: Time string (HH:MM).
  - `timeAdd`: Minutes to add to current time for default.

### f-time-counter
Display for counters, countdowns, or clocks.
- **Props:**
  - `value`: Initial value or target time.
  - `type`:
    - `0`: Counter (Days/Hours/Minutes/Seconds).
    - `1`: Countdown.
    - `2`: Real-time Clock.
  - `format`: Object defining labels for units.

## Layout & Structure Components

### fp-profile
User profile menu with avatar and actions.
- **Props:**
  - `urlAvatar`: URL for user avatar.
  - `urlAccount`: Link to account page.
  - `urlSignout`: Sign out link.
  - `urlChangePassword`: Change password link.

### header-bar
Main application header bar with navigation menus.
- **Props:**
  - `menu`: Array of top menu items.
  - `menuLeft`: Array of left sidebar menu items.
  - `logo`: Logo URL.
  - `title`: Application title.

### f-window
A dynamic dialog/window component mostly used internally by `openWindow()`.
- **Props:** `id`.

## Advanced Components

### f-chart
Wrapper for Chart.js.
- **Props:**
  - `data`: Chart data object.
  - `type`: Chart type (bar, line, pie, etc).
  - `options`: Chart.js options.

### f-chart-data-viewer
Displays chart data in a tabular/list format.
- **Props:** `label`, `data`.

### f-editor
A WYSIWYG editor (CKEditor wrapper).
- **Props:**
  - `value`: HTML content.
  - `imageapi`: Upload API endpoint.
  - `toolbar`: Custom toolbar configuration.

### f-editor-dialog
A dialog containing an `f-editor`.
- **Props:** `value`, `label`, `width`.

### f-dialog
A generic dialog generated from a JSON configuration of controls.
- **Props:**
  - `value`: Visibility boolean.
  - `data`: Data object for the form.
  - `title`: Dialog title.
  - `controls`: JSON array defining the form structure.
  - `button`: Array of action buttons.

### f-pdfmake
Renders a PDF using `pdfMake`.
- **Props:** `data` (Document Definition Object).

### f-excel-reader
A button that uploads and reads an Excel file.
- **Props:**
  - `label`: Button label.
  - `action`: Action to perform after reading.
  - `headerFormat`: Format of the header row.
