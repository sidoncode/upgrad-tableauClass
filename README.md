# 🍽️ IndiaEats Restaurant Analytics — Tableau Tutorial
### A Complete Step-by-Step Guide for Absolute Beginners

> **Whiteboard link :** https://miro.com/app/board/uXjVHPeu2mI=/?share_link_id=153055533488.
> **Project:** Analyse restaurant order data across 6 Indian cities to uncover sales trends, customer behaviour, and profit insights.
> **Dataset:** `indiaEats_data.csv` — 60 orders, 13 columns, Jan–Nov 2024
> **Level:** Complete Beginner · No prior Tableau experience needed

---

## 📁 Files in This Project

| File | What it is |
|---|---|
| `indiaEats_data.csv` | The main data file — 60 restaurant orders |
| `README.md` | This tutorial file |

---

## 🗺️ What You Will Build

By the end of this tutorial, you will have:

- ✅ Imported real data into Tableau
- ✅ Created **10 Calculated Fields** (new columns made by formulas)
- ✅ Built **4 Visualisations** (bar chart, line chart, scatter plot, pie chart)
- ✅ Understood how Tableau turns raw data into insight

---

## 📊 About the Dataset

Before touching Tableau, understand what data you have.

| Column | Type | What it means | Example |
|---|---|---|---|
| `OrderID` | Text | Unique ID for each order | ORD-001 |
| `OrderDate` | Date | When the order was placed | 2024-01-05 |
| `Branch` | Text | Which city branch | Mumbai |
| `FoodCategory` | Text | Type of cuisine | Biryani |
| `ItemName` | Text | Exact dish ordered | Chicken Biryani |
| `Quantity` | Number | How many items | 2 |
| `UnitPrice` | Number | Price of one item (₹) | 350 |
| `DeliveryTimeMins` | Number | Minutes to deliver | 35 |
| `CustomerRating` | Number | Rating out of 5 | 4.2 |
| `DeliveryType` | Text | How they received it | Home Delivery |
| `PaymentMode` | Text | How they paid | UPI |
| `CustomerAge` | Number | Age of customer | 28 |
| `IsWeekend` | Text | Was it a weekend? | Yes / No |

---

## 🚀 PART 1 — Setting Up Tableau

### Step 1: Open Tableau Desktop

1. Double-click the **Tableau Desktop** icon on your desktop.
2. The **Start Page** opens. It looks like a blue screen with connection options on the left.

> 📌 **You will see three sections on the start page:**
> - **Connect** (left panel) — where you bring in data
> - **Open** (middle) — recent workbooks
> - **Discover** (right) — sample content

---

### Step 2: Connect to Your CSV File

1. In the **Connect** panel on the LEFT side, look for **"To a File"** section.
2. Click **"Text File"**
   - 📌 Note: CSV files are text files. Don't click Excel.
3. A file browser window opens.
4. Navigate to the folder where you saved `indiaEats_data.csv`.
5. Click on `indiaEats_data.csv` to select it.
6. Click **Open**.

✅ **What you should see:** Tableau opens the **Data Source tab**. A preview table appears at the bottom showing your 60 rows of data.

---

### Step 3: Check Your Data in the Data Source Tab

Before building anything, spend 1 minute checking this screen.

Look at the **top row** — these are your column names (OrderID, OrderDate, etc.)

Look at the **icons above each column name:**
- `Abc` = Text (words, names, categories)
- `#` = Number (quantities, prices, ratings)
- 📅 = Date (order dates)
- 🌐 = Geographic (cities, countries)

**Check these carefully:**
- `OrderDate` should show a 📅 calendar icon → if it shows `Abc`, click the icon and change it to **Date**
- `Quantity`, `UnitPrice`, `DeliveryTimeMins`, `CustomerRating`, `CustomerAge` should all show `#`
- `Branch`, `FoodCategory`, `ItemName`, `DeliveryType`, `PaymentMode`, `IsWeekend` should show `Abc`

> ⚠️ **If OrderDate shows Abc:** Click the `Abc` icon above that column → select **Date** → click OK. This is important for the line chart later.

---

### Step 4: Go to the Worksheet

At the very **bottom** of your screen, you will see a tab called **Sheet 1**.
Click on it.

✅ **You are now in the worksheet — this is where you build charts.**

---

## 🗂️ PART 2 — Understanding the Tableau Workspace

Before building anything, learn these 6 key areas. Refer back to this whenever you're lost.

```
┌─────────────────────────────────────────────────────────────────────┐
│                         TOP TOOLBAR                                 │
├─────────────────────┬───────────────────────────────────────────────┤
│                     │           COLUMNS SHELF (X-axis)              │
│    DATA PANE        ├───────────────────────────────────────────────┤
│                     │           ROWS SHELF (Y-axis)                 │
│  📘 DIMENSIONS      ├───────────────────┬─────────────────────────  │
│   (Blue fields)     │                   │                           │
│   Branch            │   MARKS CARD      │      CHART CANVAS         │
│   FoodCategory      │   [Colour]        │   (Your chart appears     │
│   OrderDate...      │   [Size]          │    here after you drag    │
│                     │   [Label]         │    fields in)             │
│  📗 MEASURES        │   [Detail]        │                           │
│   (Green fields)    │   [Tooltip]       │                           │
│   Quantity          │                   │                           │
│   UnitPrice...      │                   │                           │
└─────────────────────┴───────────────────┴─────────────────────────  ┘
```

| Area | What it does |
|---|---|
| **Data Pane** (left) | Lists all your columns. Blue = categories, Green = numbers |
| **Columns shelf** (top) | Fields here become the X-axis (horizontal) |
| **Rows shelf** | Fields here become the Y-axis (vertical) |
| **Marks Card** | Controls colours, sizes, labels — how the chart looks |
| **Canvas** | The big empty area — your chart appears here |
| **Show Me** (top right button) | Suggests chart types based on what you've dragged |

> 📌 **The Golden Rule:** Drag a **blue field** to Rows/Columns to create categories. Drag a **green field** to create a number axis. Together, they make a chart.

---

## 🧮 PART 3 — Creating 10 Calculated Fields

A **Calculated Field** is a brand new column you create using a formula. It doesn't change the original file — it only exists inside Tableau.

### How to Create Any Calculated Field (Do This Each Time)

1. In the **Data Pane**, click the **small dropdown arrow (▾)** at the top right of the Data Pane.
2. Select **"Create Calculated Field..."**
3. A dialog box opens with two parts:
   - **Top field** = name your new column
   - **Large text box** = type your formula
4. Type the name and formula exactly as shown.
5. Watch the bottom of the dialog — it says **"The calculation is valid"** in green if correct.
6. Click **OK**.

> ✅ Your new field appears in the Data Pane. Green = measure (number). Blue = dimension (category).

---

### Calculated Field 1 — Total Revenue

**What it does:** Calculates how much money each order earned.

**Name:** `Total Revenue`

**Formula:**
```
[Quantity] * [UnitPrice]
```

**Step by step:**
1. Open Calculated Field dialog.
2. Type name: `Total Revenue`
3. In the formula box, type: `[Quantity] * [UnitPrice]`
   - `[Quantity]` = the Quantity column (square brackets are how Tableau refers to columns)
   - `*` = multiply
   - `[UnitPrice]` = the UnitPrice column
4. Check bottom says "The calculation is valid".
5. Click OK.

**Example:** Order ORD-001 has Quantity=2, UnitPrice=350 → Total Revenue = ₹700

---

### Calculated Field 2 — Food Cost

**What it does:** Estimates the raw ingredient cost (food industry standard: ~40% of revenue).

**Name:** `Food Cost`

**Formula:**
```
[Total Revenue] * 0.40
```

> 📌 **Tip:** You can use your own calculated fields inside new calculations! `[Total Revenue]` refers to the field you just made.

**Example:** ORD-001 Total Revenue = 700 → Food Cost = ₹280

---

### Calculated Field 3 — Gross Profit

**What it does:** Revenue minus Food Cost = actual profit per order.

**Name:** `Gross Profit`

**Formula:**
```
[Total Revenue] - [Food Cost]
```

**Example:** 700 − 280 = ₹420 profit from ORD-001

---

### Calculated Field 4 — Profit Margin %

**What it does:** Shows profit as a percentage of revenue. Tells you "out of every ₹100 earned, how much is profit?"

**Name:** `Profit Margin %`

**Formula:**
```
([Gross Profit] / [Total Revenue]) * 100
```

> 📌 **Tip:** Profit Margin % will always be 60% in this dataset because Food Cost is fixed at 40%. In real data, this varies per item.

---

### Calculated Field 5 — Revenue Category

**What it does:** Labels each order as Low, Medium, or High value. Uses an IF statement.

**Name:** `Revenue Category`

**Formula:**
```
IF [Total Revenue] >= 800 THEN "High"
ELSEIF [Total Revenue] >= 400 THEN "Medium"
ELSE "Low"
END
```

**How to read this:**
- Line 1: IF the revenue is 800 or more → label it "High"
- Line 2: ELSE IF it's between 400 and 799 → label it "Medium"
- Line 3: ELSE (anything below 400) → label it "Low"
- Line 4: END closes the IF statement (always needed)

**Example:** ORD-001 Total Revenue = 700 → Revenue Category = "Medium"

> ⚠️ **Important:** Always type `END` at the bottom of an IF formula or Tableau will show an error.

---

### Calculated Field 6 — Delivery Speed

**What it does:** Classifies each order's delivery as Fast, Normal, or Slow based on time taken.

**Name:** `Delivery Speed`

**Formula:**
```
IF [DeliveryTimeMins] <= 20 THEN "🟢 Fast"
ELSEIF [DeliveryTimeMins] <= 35 THEN "🟡 Normal"
ELSE "🔴 Slow"
END
```

> 📌 **Tip:** The emoji are optional but make the chart labels look nicer when you use this field as a colour.

**Example:** ORD-003 DeliveryTimeMins=20 → "🟢 Fast" | ORD-008 DeliveryTimeMins=45 → "🔴 Slow"

---

### Calculated Field 7 — Rating Category

**What it does:** Groups numeric ratings into named categories.

**Name:** `Rating Category`

**Formula:**
```
IF [CustomerRating] >= 4.5 THEN "Excellent"
ELSEIF [CustomerRating] >= 4.0 THEN "Good"
ELSEIF [CustomerRating] >= 3.5 THEN "Average"
ELSE "Poor"
END
```

**Example:** ORD-002 Rating=4.5 → "Excellent" | ORD-011 Rating=3.7 → "Average"

---

### Calculated Field 8 — Customer Age Group

**What it does:** Groups customers into age brackets for demographic analysis.

**Name:** `Age Group`

**Formula:**
```
IF [CustomerAge] < 25 THEN "Youth (< 25)"
ELSEIF [CustomerAge] < 35 THEN "Young Adult (25–34)"
ELSEIF [CustomerAge] < 50 THEN "Adult (35–49)"
ELSE "Senior (50+)"
END
```

**Example:** ORD-001 CustomerAge=28 → "Young Adult (25–34)"

---

### Calculated Field 9 — Revenue per Minute

**What it does:** How much revenue did this order earn per minute of delivery time? Higher = more efficient.

**Name:** `Revenue per Minute`

**Formula:**
```
[Total Revenue] / [DeliveryTimeMins]
```

**Example:** ORD-003: Revenue=450, Time=20 mins → ₹22.5 per minute

> 📌 **Why useful?** A quick cheap delivery that earns ₹450 might be more efficient than a slow expensive delivery that earns ₹700.

---

### Calculated Field 10 — Is High Value Weekend Order

**What it does:** Identifies the most valuable order type — high revenue orders placed on weekends. Uses AND logic.

**Name:** `High Value Weekend`

**Formula:**
```
IF [Total Revenue] >= 700 AND [IsWeekend] = "Yes" THEN "Yes"
ELSE "No"
END
```

**How to read this:** Only returns "Yes" if BOTH conditions are true — revenue ≥ ₹700 AND it's a weekend order.

**Example:** ORD-022: Revenue=780, IsWeekend=Yes → "Yes" | ORD-001: Revenue=700, IsWeekend=No → "No"

---

### ✅ Summary of All 10 Calculated Fields

| # | Field Name | Formula Type | Result Type |
|---|---|---|---|
| 1 | Total Revenue | Arithmetic | Number (₹) |
| 2 | Food Cost | Arithmetic | Number (₹) |
| 3 | Gross Profit | Arithmetic | Number (₹) |
| 4 | Profit Margin % | Arithmetic | Number (%) |
| 5 | Revenue Category | IF / ELSEIF | Text (Low/Medium/High) |
| 6 | Delivery Speed | IF / ELSEIF | Text (Fast/Normal/Slow) |
| 7 | Rating Category | IF / ELSEIF | Text (Excellent/Good/Average/Poor) |
| 8 | Age Group | IF / ELSEIF | Text (4 age brackets) |
| 9 | Revenue per Minute | Arithmetic | Number |
| 10 | High Value Weekend | IF + AND | Text (Yes/No) |

---

## 📈 PART 4 — Building 4 Visualisations

Before each chart, click the **"New Worksheet"** button (the small ➕ icon next to the sheet tabs at the bottom). This keeps each chart on its own clean sheet.

---

### Visualisation 1 — Bar Chart: Revenue by Food Category

**Goal:** See which food category earns the most money.
**Best for:** Comparing values across categories.

**Step 1 — Open a new sheet**
- Click the ➕ icon at the bottom → a blank Sheet 2 opens.
- Rename it: Right-click the "Sheet 2" tab → Rename → type `Revenue by Category`

**Step 2 — Build the chart**
1. Find **FoodCategory** in the Data Pane (blue, Dimensions section).
2. Drag it to the **Rows** shelf.
   - ✅ You see 6 row labels: Biryani, Chinese, Desserts, Pizza, Snacks, South Indian
3. Find **Total Revenue** in the Data Pane (green — the calculated field you made).
4. Drag it to the **Columns** shelf.
   - ✅ Tableau automatically creates a horizontal bar chart!

**Step 3 — Sort it largest to smallest**
1. Click the **Sort Descending** button in the toolbar (looks like bars going down 📊).
   - Or: Click the small sort icon that appears when you hover over "FoodCategory" on the Rows shelf.
2. ✅ Biryani should now be at the top (highest revenue).

**Step 4 — Add colour by Category**
1. Drag **FoodCategory** from the Data Pane onto the **Colour** box in the Marks card.
2. ✅ Each bar gets a different colour.

**Step 5 — Add labels to show the exact numbers**
1. Drag **Total Revenue** from the Data Pane onto the **Label** box in the Marks card.
2. ✅ Numbers appear at the end of each bar.

**Step 6 — Add a title**
1. Double-click the "Sheet 2" title area at the top of the chart canvas.
2. Type: `Total Revenue by Food Category`
3. Press Enter.

**Step 7 — Format the numbers as currency**
1. Right-click the X-axis (the numbers at the bottom) → **Format**.
2. In the Format panel, under **Numbers** → click the dropdown → select **Currency (Custom)**.
3. Set prefix to `₹`, decimal places to `0`.

> 📌 **What to observe:** Biryani dominates revenue because it has the highest unit prices and good order quantities. Snacks have many orders but low revenue because unit prices are low.

---

### Visualisation 2 — Line Chart: Monthly Revenue Trend

**Goal:** See how revenue changes month by month across 2024.
**Best for:** Showing trends over time.

**Step 1 — Open a new sheet**
- Click ➕ → rename to `Monthly Revenue Trend`

**Step 2 — Place Order Date on the X-axis**
1. Find **OrderDate** in the Data Pane (it's in the Dimensions section with a 📅 icon).
2. Drag it to the **Columns** shelf.
3. ⚠️ By default, Tableau shows `YEAR(Order Date)` — just one point for 2024. That's not useful.
4. To fix this: **Right-click** the `YEAR(Order Date)` pill on the Columns shelf.
5. In the dropdown, look for **"Month"** — there are TWO Month options:
   - First "Month" = groups all Januaries together (don't use this)
   - Second "Month" (at the bottom of the list) = shows each month individually ← **use this one**
6. Click the **second "Month"** option.
7. ✅ The pill now shows `MONTH(Order Date)` and you see Jan, Feb, Mar... on the X-axis.

**Step 3 — Place Total Revenue on the Y-axis**
1. Drag **Total Revenue** to the **Rows** shelf.
2. ✅ A line chart appears showing monthly revenue!

**Step 4 — Make it look like a proper line chart**
1. Look at the Marks card — the dropdown at the top should say "Automatic" or "Bar".
2. Click that dropdown → select **Line**.
3. ✅ Bars become a connected line.

**Step 5 — Add data point markers**
1. Click **Colour** in the Marks card.
2. In the popup, find **"Markers"** → select the filled circle option.
3. ✅ Small dots appear at each month's data point.

**Step 6 — Add labels on the line**
1. Drag **Total Revenue** onto **Label** in the Marks card.
2. ✅ Revenue numbers appear above each data point.

**Step 7 — Add a reference line for average**
1. Right-click the Y-axis (the numbers on the left) → **"Add Reference Line"**.
2. In the dialog, keep **Value = Average** and **Line = Dashed**.
3. Click OK.
4. ✅ A dashed horizontal line shows the average monthly revenue.

> 📌 **What to observe:** Revenue should be fairly consistent Jan–Aug (6 orders/month), with Oct looking strong (Diwali season). Nov looks lower because the dataset only has 2 November orders.

---

### Visualisation 3 — Scatter Plot: Delivery Time vs Customer Rating

**Goal:** See if faster deliveries lead to better customer ratings.
**Best for:** Showing the relationship between two numbers.

**Step 1 — Open a new sheet**
- Click ➕ → rename to `Delivery Time vs Rating`

**Step 2 — Place Delivery Time on X-axis**
1. Drag **DeliveryTimeMins** to the **Columns** shelf.
2. ✅ A single axis appears at the bottom (0 to 50 minutes).

**Step 3 — Place Customer Rating on Y-axis**
1. Drag **CustomerRating** to the **Rows** shelf.
2. ✅ Tableau creates a scatter plot with many overlapping dots!
3. Right now you see one big dot — that's because Tableau aggregated everything. Fix this next.

**Step 4 — Show individual orders (not aggregates)**
1. Drag **OrderID** from the Data Pane onto **Detail** in the Marks card.
2. ✅ Each order is now its own separate dot — 60 dots appear.

**Step 5 — Colour dots by Delivery Speed**
1. Drag your calculated field **Delivery Speed** onto **Colour** in the Marks card.
2. ✅ Dots are now coloured: Green = Fast, Yellow = Normal, Red = Slow.

**Step 6 — Size dots by Total Revenue**
1. Drag **Total Revenue** onto **Size** in the Marks card.
2. ✅ Higher-value orders appear as larger dots.

**Step 7 — Add a Trend Line to see the pattern**
1. Go to the top menu → **Analysis** → **Trend Lines** → **Show Trend Lines**.
2. ✅ A diagonal line appears showing the overall trend.
3. Hover over the trend line to see its statistics.

**Step 8 — Customise tooltips**
1. Click **Tooltip** in the Marks card.
2. In the editor, type:
   ```
   Order: <OrderID>
   Delivery Time: <AVG(DeliveryTimeMins)> mins
   Rating: <AVG(CustomerRating)>
   Speed: <Delivery Speed>
   ```
3. Click OK.
4. ✅ Hovering over any dot shows a clean informative popup.

> 📌 **What to observe:** The trend line should slope downward from left to right — meaning longer delivery times tend to produce lower ratings. Fast deliveries (green) cluster in the top-left (fast + high rating). Slow deliveries (red) tend toward the bottom-right.

---

### Visualisation 4 — Pie Chart: Revenue Share by Delivery Type

**Goal:** See what proportion of revenue comes from Home Delivery vs Dine-in vs Takeaway.
**Best for:** Showing part-to-whole (what percentage each piece is).

**Step 1 — Open a new sheet**
- Click ➕ → rename to `Revenue by Delivery Type`

**Step 2 — Drag Total Revenue to the canvas**
1. Drag **Total Revenue** to the **Rows** shelf.
2. A single bar appears.

**Step 3 — Switch to Pie chart via Show Me**
1. Click **Show Me** button in the top-right corner of Tableau.
2. Click on the **Pie chart** icon (it looks like a circle divided into slices).
3. ✅ Tableau builds a basic pie chart.
4. Close the Show Me panel (click Show Me again).

**Step 4 — Colour slices by Delivery Type**
1. Drag **DeliveryType** onto **Colour** in the Marks card.
2. ✅ Three slices appear: Home Delivery, Dine-in, Takeaway.

**Step 5 — Add labels showing % and category**
1. Drag **DeliveryType** onto **Label** in the Marks card.
2. Click **Label** in the Marks card.
3. Tick "Show mark labels".
4. In the label text box, click **Insert** → select **Percent of Total**.
5. Edit the label to show:
   ```
   <DeliveryType>
   <Percent of Total>
   ```
6. Click OK.
7. ✅ Each slice shows its label and percentage.

**Step 6 — Make the pie chart bigger**
1. Press **Ctrl + Shift + B** (Windows) or **Command + Shift + B** (Mac) to fit the view.
2. Or: Go to menu **View → Fit → Entire View**.

**Step 7 — Customise slice colours**
1. Click **Colour** in the Marks card.
2. Click **Edit Colours**.
3. Click on each category to change its colour — use warm, food-friendly colours.
4. Click OK.

> 📌 **What to observe:** Home Delivery likely has the largest slice (many orders in our dataset). Dine-in orders tend to have higher ratings (no wait anxiety). Takeaway falls in between.

---

## 📐 PART 5 — Formatting Tips for All Charts

Apply these to polish each chart:

**Remove gridlines (cleaner look):**
- Format → Shading → Set Row Banding to None

**Change font sizes:**
- Format → Font → change Worksheet font size

**Hide the field name on an axis:**
- Right-click the axis → Edit Axis → uncheck "Show axis title"

**Add borders to the chart:**
- Worksheet menu → Format → Border

**Rename a field label in the chart:**
- Right-click the field in the Data Pane → Rename → type new name

---

## 🏆 PART 6 — Quick Formula Reference

Use these inside Calculated Fields:

| Formula | What it does | Example |
|---|---|---|
| `[A] + [B]` | Add | `[Gross Profit] + [Tax]` |
| `[A] - [B]` | Subtract | `[Revenue] - [Cost]` |
| `[A] * [B]` | Multiply | `[Quantity] * [UnitPrice]` |
| `[A] / [B]` | Divide | `[Profit] / [Revenue]` |
| `IF ... THEN ... END` | Conditional | See CF 5–10 above |
| `ROUND([A], 2)` | Round to 2 decimals | `ROUND([Margin], 2)` |
| `ABS([A])` | Remove negative sign | `ABS([Loss])` |
| `UPPER([A])` | Make text UPPERCASE | `UPPER([Branch])` |
| `LEN([A])` | Count characters in text | `LEN([ItemName])` |
| `TODAY()` | Today's date | Use in date formulas |
| `DATEDIFF('day', [A], TODAY())` | Days since a date | Days since order |
| `DATEPART('month', [A])` | Extract month number | `DATEPART('month', [OrderDate])` |
| `MIN([A], [B])` | Smaller of two values | — |
| `MAX([A], [B])` | Larger of two values | — |
| `ISNULL([A])` | Check if value is empty | Use in IF to handle blanks |
| `ZN([A])` | Replace NULL with 0 | `ZN([Discount])` |

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + Z` | Undo |
| `Ctrl + S` | Save workbook |
| `Ctrl + D` | Duplicate sheet |
| `Ctrl + W` | Swap Rows and Columns |
| `Ctrl + Shift + B` | Fit to window |
| `F7` | Presentation mode |
| `Ctrl + E` | Edit calculated field |
| `Ctrl + 1` | Open Show Me panel |

---

## ❓ Common Beginner Mistakes & Fixes

| Problem | What went wrong | Fix |
|---|---|---|
| Chart shows only 1 bar/line | Tableau is aggregating everything | Drag a dimension (blue) to Rows to split it |
| Numbers show "SUM" in formula | Normal — Tableau auto-aggregates measures | This is correct behaviour |
| "Invalid calculation" error | Formula has a typo or missing END | Check brackets, spelling, and END on IF statements |
| Date shows as year only | Tableau defaults to year level | Right-click date pill → choose Month/Day |
| Chart looks empty | Wrong field type | Check Dimensions vs Measures — numbers should be green |
| Pie chart not showing | Need at least one measure and one dimension | Drag Total Revenue + DeliveryType, then use Show Me |

---

## 🎓 You're Done!

You have now:
- ✅ Imported `indiaEats_data.csv` into Tableau
- ✅ Created **10 Calculated Fields** using arithmetic and IF logic
- ✅ Built a **Bar Chart** (Revenue by Category)
- ✅ Built a **Line Chart** (Monthly Revenue Trend)
- ✅ Built a **Scatter Plot** (Delivery Time vs Rating)
- ✅ Built a **Pie Chart** (Revenue by Delivery Type)

**Next steps to explore:**
- Combine all 4 charts into a **Dashboard**
- Add **Filters** (e.g., filter by Branch or Month)
- Try **Parameters** to let users pick a Top N category
- Explore **Table Calculations** like Running Total and % Difference

---

*Dataset: IndiaEats Restaurant Analytics | 60 Orders | Jan–Nov 2024 | 6 Cities*
