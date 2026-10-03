# Phase 1: Excel Foundations

> **Goal:** Get comfortable with the Excel interface, enter and format data correctly, write basic formulas, and organize data with sorting and filtering.

## Progress Checklist

- [ ] 1. Interface and basic terms
- [ ] 2. Entering and formatting data
- [ ] 3. Basic formulas and functions
- [ ] 4. Cell references (relative, absolute, mixed)
- [ ] 5. Keyboard shortcuts
- [ ] 6. Sorting, filtering, Freeze Panes, Find & Replace
- [ ] 7. Practice project: Monthly Expense Tracker

---

## 1. Interface and Basic Terms

| Term | Meaning |
|------|---------|
| **Workbook** | An entire Excel file (`.xlsx`) |
| **Worksheet** | A single tab (sheet) inside a workbook |
| **Cell** | One box, identified by column letter + row number (e.g., `B3`) |
| **Range** | A group of cells (e.g., `A1:C10`) |
| **Formula Bar** | Shows the content or formula of the selected cell |
| **Name Box** | Shows the address of the selected cell; type an address here to jump to it |
| **Ribbon** | The top toolbar (Home, Insert, Formulas, Data, View, etc.) |
| **Active Cell** | The currently selected cell |

### Useful Basics
- Rename a sheet: double-click the tab
- Add a sheet: click the `+` next to the tabs
- Move/copy a sheet: right-click the tab, then Move or Copy
- Column width auto-fit: double-click the border between two column headers

---

## 2. Entering and Formatting Data

### Data Types

| Type | Example | Notes |
|------|---------|-------|
| Text | `Pen`, `Delhi` | Left-aligned by default |
| Number | `250`, `3.14` | Right-aligned by default |
| Date | `03-10-2026` | Stored internally as a number |
| Currency | `₹1,500.00` | Number with a currency format |
| Percentage | `18%` | `0.18` shown as 18% |

> **Tip:** If a number is left-aligned, it is probably stored as text. This is a common cause of formula errors.

### Formatting (Ctrl+1 opens Format Cells)
- **Number tab:** General, Number, Currency, Date, Percentage, Text
- **Alignment:** left/center/right, wrap text, merge & center (use sparingly)
- **Font and fill color:** for headers and emphasis
- **Borders:** to separate sections of a table

### Fill Handle
Drag the small square at the bottom-right of a cell to:
- Copy values
- Continue a series (1, 2, 3 / Jan, Feb, Mar / Mon, Tue, Wed)
- Copy a formula down

---

## 3. Basic Formulas and Functions

Every formula starts with `=`.

### Arithmetic Operators
`+`  `-`  `*`  `/`  `^` (power)

Example: `=A1+B1`, `=A1*B1`, `=A1^2`

### Core Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `SUM` | Adds numbers | `=SUM(B2:B10)` |
| `AVERAGE` | Mean of numbers | `=AVERAGE(B2:B10)` |
| `MIN` | Smallest value | `=MIN(B2:B10)` |
| `MAX` | Largest value | `=MAX(B2:B10)` |
| `COUNT` | Counts cells with numbers | `=COUNT(B2:B10)` |
| `COUNTA` | Counts non-empty cells | `=COUNTA(A2:A10)` |
| `COUNTBLANK` | Counts empty cells | `=COUNTBLANK(A2:A10)` |

### Order of Operations (BODMAS)
Brackets, Orders (powers), Division/Multiplication, Addition/Subtraction.

Example: `=2+3*4` gives 14, but `=(2+3)*4` gives 20.

### AutoSum
Select a cell below a column of numbers and press **Alt + =** to insert `SUM` automatically.

### Common Errors

| Error | Meaning |
|-------|---------|
| `#DIV/0!` | Dividing by zero or an empty cell |
| `#VALUE!` | Wrong data type (e.g., adding text to a number) |
| `#NAME?` | Misspelled function name |
| `#REF!` | A referenced cell was deleted |
| `#N/A` | Value not found (common in lookups) |
| `####` | Column is too narrow to show the value |

---

## 4. Cell References

| Type | Example | Behavior when copied |
|------|---------|----------------------|
| **Relative** | `A1` | Changes based on the new position |
| **Absolute** | `$A$1` | Never changes |
| **Mixed** | `$A1` or `A$1` | Locks only the column or only the row |

**Shortcut:** Press **F4** while editing a formula to cycle through `A1` → `$A$1` → `A$1` → `$A1`.

### Example: Tax Calculation
| | A | B | C |
|---|---|---|---|
| 1 | **Tax Rate** | 18% | |
| 2 | **Item** | **Price** | **Tax** |
| 3 | Pen | 10 | `=B3*$B$1` |
| 4 | Book | 200 | `=B4*$B$1` |

`$B$1` stays fixed when you copy the formula down, while `B3` changes to `B4`.

### Referencing Other Sheets
`=Sheet2!A1` or `=SUM(Sheet2!B2:B10)`

---

## 5. Keyboard Shortcuts

### Navigation and Selection

| Shortcut | Action |
|----------|--------|
| `Ctrl + Arrow` | Jump to the edge of data |
| `Ctrl + Shift + Arrow` | Select to the edge of data |
| `Ctrl + Home` | Go to A1 |
| `Ctrl + A` | Select all |
| `Ctrl + Space` | Select the entire column |
| `Shift + Space` | Select the entire row |

### Editing

| Shortcut | Action |
|----------|--------|
| `F2` | Edit the active cell |
| `Ctrl + Z` / `Ctrl + Y` | Undo / Redo |
| `Ctrl + C` / `Ctrl + V` / `Ctrl + X` | Copy / Paste / Cut |
| `Ctrl + D` | Fill down |
| `Ctrl + R` | Fill right |
| `Ctrl + ;` | Insert today's date |
| `Ctrl + Shift + ;` | Insert current time |
| `Ctrl + +` / `Ctrl + -` | Insert / Delete cells, rows, columns |

### Formatting and Tools

| Shortcut | Action |
|----------|--------|
| `Ctrl + 1` | Format Cells |
| `Ctrl + B` / `Ctrl + I` / `Ctrl + U` | Bold / Italic / Underline |
| `Alt + =` | AutoSum |
| `Ctrl + T` | Convert range to an Excel Table |
| `Ctrl + Shift + L` | Toggle filters |
| `Ctrl + F` / `Ctrl + H` | Find / Replace |
| `F4` | Toggle reference type (or repeat last action) |

---

## 6. Sorting, Filtering, Freeze Panes, Find & Replace

### Sorting (Data tab → Sort)
- **Single-level:** sort by one column (A to Z, smallest to largest)
- **Multi-level:** e.g., sort by Region, then by Sales (largest to smallest)
- Always select the whole table, or click inside it, so rows stay intact
- Make sure "My data has headers" is ticked

### Filtering (Ctrl + Shift + L)
- Filter by value, text condition (contains, begins with), number condition (greater than), or date
- Use **Clear** to remove filters without deleting data

### Freeze Panes (View tab)
- **Freeze Top Row:** keeps headers visible while scrolling
- **Freeze First Column:** keeps IDs/names visible
- **Freeze Panes:** select the cell *below and right* of what you want to freeze

### Find & Replace (Ctrl + F / Ctrl + H)
- Search within a sheet or the whole workbook
- Use wildcards: `*` for any characters, `?` for a single character
- Click **Options** to match case or search in formulas

---

## 7. Practice Project: Monthly Expense Tracker

**Build a workbook with:**
1. A table with columns: `Date`, `Category`, `Description`, `Amount`, `Payment Mode`
2. At least 30 sample entries across a month
3. A summary area using `SUM`, `AVERAGE`, `MIN`, `MAX`, and `COUNT`
4. A tax or savings calculation using an **absolute reference**
5. Formatting: currency format, bold headers, borders, fill color
6. Freeze the header row, add filters, and sort by Amount (largest to smallest)

**Stretch goal:** Add a second sheet for another month and reference its totals from a "Summary" sheet.

---

## Common Mistakes to Avoid
- Typing numbers with symbols (like `Rs.`) directly, instead of using Currency format
- Merging cells in data tables, since it breaks sorting and filtering
- Forgetting `$` when a reference should be locked
- Leaving blank rows or columns inside a dataset
- Hard-coding numbers inside formulas instead of referencing cells

---

