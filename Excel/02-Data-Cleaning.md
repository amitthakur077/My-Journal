# Phase 2: Data Cleaning 

> **Goal:** Take messy, real-world data and turn it into clean, consistent, analysis-ready data using text functions, built-in cleaning tools, error handling, data validation, and date functions.

## Progress Checklist

- [ ] 1. Why data cleaning matters
- [ ] 2. Text functions
- [ ] 3. Text to Columns, Flash Fill, Remove Duplicates
- [ ] 4. Handling blanks and errors
- [ ] 5. Data Validation
- [ ] 6. Date functions
- [ ] 7. Practice project: Clean a messy dataset

---

## 1. Why Data Cleaning Matters

Analysts often spend most of their time cleaning data. Wrong or inconsistent data leads to wrong conclusions.

### Typical Problems in Messy Data

| Problem | Example |
|---------|---------|
| Extra spaces | `" Delhi "` |
| Inconsistent case | `delhi`, `DELHI`, `Delhi` |
| Duplicates | Same customer entered twice |
| Blanks | Missing phone numbers |
| Numbers stored as text | `"250"` instead of `250` |
| Mixed date formats | `03/10/2026`, `3-Oct-26` |
| Combined fields | `"Rahul Sharma"` in one cell |
| Typos and spelling variants | `Punjab`, `Panjab`, `PB` |

### Golden Rules
1. **Never clean the original data.** Work on a copy of the sheet.
2. Keep the raw data on its own sheet, untouched.
3. Document what you changed (a small "Cleaning Log" sheet or notes).

---

## 2. Text Functions

| Function | Purpose | Example | Result |
|----------|---------|---------|--------|
| `TRIM` | Removes extra spaces (keeps single spaces between words) | `=TRIM("  Hello   World ")` | `Hello World` |
| `CLEAN` | Removes non-printable characters | `=CLEAN(A2)` | Clean text |
| `UPPER` | Converts to uppercase | `=UPPER("delhi")` | `DELHI` |
| `LOWER` | Converts to lowercase | `=LOWER("DELHI")` | `delhi` |
| `PROPER` | Capitalizes each word | `=PROPER("rahul sharma")` | `Rahul Sharma` |
| `LEN` | Counts characters | `=LEN("Excel")` | `5` |
| `LEFT` | Extracts from the start | `=LEFT("Excel",2)` | `Ex` |
| `RIGHT` | Extracts from the end | `=RIGHT("Excel",3)` | `cel` |
| `MID` | Extracts from the middle | `=MID("Excel",2,3)` | `xce` |
| `FIND` | Position of text (case-sensitive) | `=FIND("c","Excel")` | `4` |
| `SEARCH` | Position of text (not case-sensitive) | `=SEARCH("C","Excel")` | `4` |
| `SUBSTITUTE` | Replaces specific text | `=SUBSTITUTE("a-b-c","-","/")` | `a/b/c` |
| `REPLACE` | Replaces by position | `=REPLACE("Excel",1,2,"XX")` | `XXcel` |
| `CONCAT` | Joins text | `=CONCAT(A2," ",B2)` | `Rahul Sharma` |
| `TEXTJOIN` | Joins with a delimiter, can skip blanks | `=TEXTJOIN(", ",TRUE,A2:C2)` | `Delhi, Punjab, Goa` |
| `VALUE` | Converts text to a number | `=VALUE("250")` | `250` |
| `TEXT` | Formats a value as text | `=TEXT(A2,"dd-mmm-yyyy")` | `03-Oct-2026` |

### Combining Functions (Very Common)

**Clean and standardize a name:**
```excel
=PROPER(TRIM(A2))
```

**Extract the first name from "Rahul Sharma":**
```excel
=LEFT(A2, FIND(" ", A2) - 1)
```

**Extract the last name:**
```excel
=MID(A2, FIND(" ", A2) + 1, LEN(A2))
```

**Remove a non-breaking space (common in web-copied data):**
```excel
=TRIM(SUBSTITUTE(A2, CHAR(160), " "))
```

> **Tip:** After cleaning with formulas, copy the results and use **Paste Special → Values** (`Ctrl + Alt + V`, then `V`) to replace the formulas with clean static values.

---

## 3. Built-in Cleaning Tools

### Text to Columns (Data tab)
Splits one column into several using a delimiter (comma, space, hyphen) or fixed width.

**Steps:**
1. Select the column
2. Data → Text to Columns
3. Choose **Delimited** (or Fixed width)
4. Pick the delimiter
5. Choose the destination cell so you do not overwrite other data
6. Finish

**Use cases:** splitting full names, splitting "City, State", splitting dates stored as text.

### Flash Fill (`Ctrl + E`)
Excel detects a pattern from your example and fills the rest.

**Steps:**
1. Type the desired result in the first row (e.g., `Rahul` next to `Rahul Sharma`)
2. Start the second row, or press `Ctrl + E`
3. Review the results carefully

> **Caution:** Flash Fill gives static values (not formulas) and can misread patterns, so always check the output.

### Remove Duplicates (Data tab)
1. Select the data
2. Data → Remove Duplicates
3. Choose the columns that define a duplicate
4. Click OK

> **Tip:** Before deleting, highlight duplicates first: Home → Conditional Formatting → Highlight Cells Rules → Duplicate Values. Always work on a copy.

### Other Quick Cleaning Tools
- **Find & Replace** (`Ctrl + H`) for fixing spelling variants in bulk
- **Go To Special** (`F5` → Special → Blanks) to select all blank cells at once
- **Convert text-numbers to numbers:** select the cells, click the warning icon, choose "Convert to Number"
- **Sort and Filter** to spot outliers and odd entries
- **Text filters:** "Does not contain", "Begins with", to find inconsistencies

---

## 4. Handling Blanks and Errors

### Checking for Blanks and Types

| Function | Purpose | Example |
|----------|---------|---------|
| `ISBLANK` | TRUE if the cell is empty | `=ISBLANK(A2)` |
| `ISNUMBER` | TRUE if the value is a number | `=ISNUMBER(A2)` |
| `ISTEXT` | TRUE if the value is text | `=ISTEXT(A2)` |
| `ISERROR` | TRUE if the value is any error | `=ISERROR(A2)` |
| `ISNA` | TRUE if the error is `#N/A` | `=ISNA(A2)` |

### IFERROR
Replaces an error with a value you choose.

```excel
=IFERROR(A2/B2, 0)
=IFERROR(A2/B2, "Check data")
```

### Handling Blanks with IF
```excel
=IF(ISBLANK(A2), "Missing", A2)
=IF(A2="", "Not provided", A2)
```

### Ways to Treat Missing Data

| Approach | When to use |
|----------|-------------|
| Delete the row | Few blanks, and the row has little value |
| Fill with a default (e.g., "Unknown", 0) | Categories or counts |
| Fill with the average/median | Numeric columns where a reasonable estimate is acceptable |
| Leave blank and flag it | When blanks themselves carry meaning |

> **Note:** Do not fill blanks blindly. Always ask why the data is missing.

---

## 5. Data Validation

Prevents bad data from being entered in the first place.

**Path:** Data → Data Validation

### Common Validation Types

| Type | Use |
|------|-----|
| **List** | Dropdown menu (e.g., Yes/No, categories) |
| **Whole number** | Only integers within a range (e.g., age 18-60) |
| **Decimal** | Numbers with decimals within limits |
| **Date** | Dates within a range |
| **Text length** | Limits characters (e.g., a 10-digit phone number) |
| **Custom** | Uses a formula (e.g., `=COUNTIF($A:$A,A2)=1` for unique entries) |

### Creating a Dropdown List
1. Select the cells
2. Data → Data Validation → Allow: **List**
3. Source: type values separated by commas (`Yes,No`) or select a range
4. Use the **Input Message** tab to guide users and the **Error Alert** tab to show a custom warning

### Useful Extras
- **Circle Invalid Data:** Data Validation dropdown → Circle Invalid Data (finds existing bad entries)
- **Dependent dropdowns:** use named ranges with `INDIRECT` (covered later)

---

## 6. Date Functions

Excel stores dates as serial numbers (1 = 1 Jan 1900), so you can do arithmetic with them.

| Function | Purpose | Example |
|----------|---------|---------|
| `TODAY` | Current date | `=TODAY()` |
| `NOW` | Current date and time | `=NOW()` |
| `DATE` | Builds a date | `=DATE(2026,10,3)` |
| `YEAR` | Extracts the year | `=YEAR(A2)` |
| `MONTH` | Extracts the month number | `=MONTH(A2)` |
| `DAY` | Extracts the day | `=DAY(A2)` |
| `WEEKDAY` | Day of the week as a number | `=WEEKDAY(A2,2)` |
| `EOMONTH` | End of a month, offset by N months | `=EOMONTH(A2,0)` |
| `EDATE` | Same day, N months later | `=EDATE(A2,3)` |
| `DATEDIF` | Difference between dates | `=DATEDIF(A2,TODAY(),"Y")` |
| `NETWORKDAYS` | Working days between two dates | `=NETWORKDAYS(A2,B2)` |
| `DATEVALUE` | Converts a text date to a real date | `=DATEVALUE("03-Oct-2026")` |

### DATEDIF Units

| Unit | Returns |
|------|---------|
| `"Y"` | Complete years |
| `"M"` | Complete months |
| `"D"` | Days |
| `"YM"` | Months ignoring years |
| `"MD"` | Days ignoring months and years |

**Calculate age:**
```excel
=DATEDIF(B2, TODAY(), "Y")
```

**Get the month name:**
```excel
=TEXT(A2, "mmmm")
```

> **Common problem:** Dates imported as text (left-aligned) will not calculate. Use `DATEVALUE`, Text to Columns (choose a Date format in the last step), or Find & Replace to fix separators.

---

## 7. Practice Project: Clean a Messy Dataset

**Dataset:** Download a messy sales, customer, or employee dataset from Kaggle (search for "messy data", "dirty data", or "data cleaning practice").

**Tasks:**
1. Copy the raw data to a new sheet named `Raw_Data` and leave it untouched
2. Create a `Cleaned_Data` sheet
3. Fix extra spaces and inconsistent capitalization using `TRIM` and `PROPER`
4. Split a full name into first and last name
5. Find and remove duplicate records
6. Identify blanks and decide how to treat each one
7. Convert text-numbers and text-dates into real numbers and dates
8. Standardize spelling variants with Find & Replace
9. Add a dropdown (Data Validation) for a category column
10. Calculate Age or Tenure with `DATEDIF`
11. Wrap risky formulas in `IFERROR`
12. Add a `Cleaning_Log` sheet describing every change you made

**Stretch goal:** Record before/after row counts and the number of errors fixed, and add them to your README as a mini case study.

---

## Common Mistakes to Avoid
- Cleaning the only copy of your data
- Forgetting to Paste Special → Values before deleting the helper columns
- Using `TRIM` and expecting it to remove non-breaking spaces (use `SUBSTITUTE` with `CHAR(160)`)
- Removing duplicates based on the wrong columns
- Filling blanks with 0 when 0 has a real meaning
- Trusting Flash Fill without checking the results

---

## Quick Reference: Cleaning Workflow

1. **Inspect** the data (filters, sorting, scrolling, `COUNTBLANK`)
2. **Copy** the raw data to a backup sheet
3. **Fix structure** (split or merge columns, fix data types)
4. **Fix content** (spaces, case, spelling, duplicates)
5. **Handle blanks and errors**
6. **Validate** (dropdowns, rules, spot checks)
7. **Document** what you changed

---
