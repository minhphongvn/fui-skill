# Advanced FUI Techniques

This document captures advanced patterns and techniques for FUI development, extracted from real-world implementations.

## 1. Advanced Logic & Scripting

FUI's JSON-based logic has limitations. Use `script.js` for complex operations.

### Computed Properties Workaround
FUI `module.json` does not natively support computed properties. 
**Solution:** Define calculation functions in `script.js` and call them directly in `module.json`.

**script.js**:
```javascript
function getTongTien() {
    return vueData.items.reduce((sum, item) => sum + (item.amount || 0), 0);
}
```

**module.json**:
```json
{
  "innerHTML": "Total: {{getTongTien().toLocaleString()}} VNĐ"
}
```

### Complex Validation
Avoid writing long logic strings in JSON. Move validation logic to `script.js`.

**script.js**:
```javascript
function validateStep1() {
    const d = vueData;
    if (!d.name || !d.email) {
        alert("Missing required fields!");
        return false;
    }
    return true;
}

function nextStep() {
    if (vueData.step === 1 && !validateStep1()) return;
    vueData.step++;
}
```

**module.json**:
```json
"v-on:click": "nextStep()"
```

### Action Binding
You can bind direct JS functions to events instead of using the `CALL` action protocol if needed for simple UI logic.

```json
"v-on:click": "prevBuoc()"
```

---

## 2. PDF Generation (pdfmake)

Techniques for generating complex PDFs using `pdfmake` within FUI.

### Dynamic Tables
Map array data to table rows dynamically.

```javascript
/* script.js */
body: [
    [{ text: 'STT', bold: true }, { text: 'Name', bold: true }],
    ...data.items.map(item => ([
        item.index,
        item.name
    ]))
]
```

### SVG Checkboxes
Unicode characters (☑/☐) may fail to render in some PDF fonts. Use SVG paths instead.

```javascript
const checkedSvg = '<svg ...>...</svg>';
const uncheckedSvg = '<svg ...>...</svg>';

{
    svg: item.isChecked ? checkedSvg : uncheckedSvg,
    width: 14
}
```

### Complex Layouts
Use `columns` for layouts that standard tables can't handle easily (like checkboxes side-by-side with text).

```javascript
{
    columns: [
        { svg: checkedSvg, width: 14 },
        { text: ' Label text', width: '*' }
    ]
}
```

### Signature Section Table
Use a nested table structure for signature blocks to ensure alignment.

```javascript
table: {
    widths: ['16%', '16%', ...], // 6 columns
    body: [
        [{ text: 'Title', colSpan: 3 }, {}, {} ...], // Header spanning columns
        ['Sign 1', 'Sign 2', ...] // Individual signature slots
    ]
}
```
