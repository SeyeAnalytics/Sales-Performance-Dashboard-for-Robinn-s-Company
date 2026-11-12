# Sales-Performance-Dashboard-for-Robinn-s-Company
An interactive Power BI report that turns **$24.9M** of sales into one screen: who buys, where, what, and how revenue moved from **January 2015 to June 2017**.

<img width="1152" height="574" alt="dashboard-full" src="https://github.com/user-attachments/assets/71c5760c-084e-4fcb-b723-8ed6b80bcca3" />


| | |
|---|---|
| **Tool** | Power BI |
| **Skills** | Data cleaning (Power Query), data modelling, DAX, dashboard design |
| **Period covered** | Jan 2015 – Jun 2017 |

---

## Business problem

Leadership at Robinn's Company had sales data but no quick way to see what was driving revenue. The dashboard answers five questions:

1. How are we doing overall? (revenue, profit, returns, units sold)
2. Who is buying? (customer occupation and gender)
3. Where is the money coming from? (revenue by region)
4. What are we selling? (revenue by product category)
5. Is the business growing? (monthly trend and pace of change)

---

## Methodology

1. **Understand and profile the data.** Reviewed the sales, customer, product, region and returns tables to learn what each row represents, check for blanks and duplicates, and confirm the date range.
2. **Clean and shape in Power Query.** Fixed data types, standardised text fields, handled missing values (for example, customers with no gender recorded, shown as NA) and removed duplicates.
3. **Build the data model.** Connected one central sales table to dimension tables for customers, products and categories, regions, and a calendar table (star schema), so that selecting a region updates every visual.
4. **Write DAX measures.** Each KPI is a measure, not a calculated column, so it responds to whatever the viewer filters. Examples:

   ```DAX
   Total Revenue   = SUM ( Sales[Revenue] )
   Total Profit    = [Total Revenue] - SUM ( Sales[Cost] )
   Profit Margin % = DIVIDE ( [Total Profit], [Total Revenue] )
   Revenue MoM %   = VAR prev = CALCULATE ( [Total Revenue], DATEADD ( 'Date'[Date], -1, MONTH ) )
                     RETURN DIVIDE ( [Total Revenue] - prev, prev )
   ```
5. **Choose visuals for the question.** Cards for headline numbers, horizontal bars for ranked categories, a donut for a two-way split, columns for regions, a line for time, and a smart narrative box to state the main movements in words.
6. **Design for readability.** Warm two-colour palette, large KPI figures, data labels on every chart, and a region slicer so managers can filter without training.
7. **Validate.** Reconciled KPI cards against table totals, checked that the occupation and region breakdowns add back up to total revenue, and tested the slicer on each region.

---

## Dashboard walkthrough

### Headline KPIs

<img width="2304" height="180" alt="kpi" src="https://github.com/user-attachments/assets/7374c5d1-b3d5-44bd-9798-94a38f81336b" />


| Metric | Value | What it means |
|---|---|---|
| Total revenue | $24.91M | All sales across the period |
| Total profit | $10.46M | About 42% of revenue, a healthy margin |
| Total returns | 1,828 | A cost signal worth tracking by product and region |
| Quantities sold | 84K | Roughly $300 of revenue per unit, which fits a high-ticket product like bikes |

### Revenue by customer occupation

<img width="800" height="416" alt="occupation" src="https://github.com/user-attachments/assets/6ac221c3-e551-4968-84e1-c552d55de490" />


Professionals lead with **$8.5M** (about 34% of revenue), followed by Skilled Manual ($5.4M), Management ($4.6M), Clerical ($4.0M) and Manual ($2.5M). Professional and Skilled Manual customers together bring in over half of all sales.

**So what:** marketing should lean toward these two groups, and Manual customers are the clearest room for growth.

### Revenue by gender

<img width="796" height="416" alt="gender" src="https://github.com/user-attachments/assets/6db2d7e5-815d-4eeb-91c9-4bf9e1cde78b" />


Revenue is almost perfectly balanced: **50.23% female** and **49.14% male**. The remaining 0.63% has no gender recorded.

**So what:** gender is not a useful targeting lever here. The NA slice is small but flags a data-capture gap to fix at source.

### Revenue by region

<img width="700" height="416" alt="region" src="https://github.com/user-attachments/assets/0f4260a7-d7aa-47a7-a9eb-f6f82b730d30" />


Australia is the largest market at **$7.4M** (about 30%), then Southwest ($4.8M) and Northwest ($3.1M). These three regions generate roughly **61%** of revenue. The UK, Germany, France and Canada follow between $1.8M and $2.9M. Southeast, Northeast and Central show about $0.0M.

**So what:** revenue is concentrated in a few markets. The three near-zero regions need checking to see whether they are genuinely tiny or a data gap.

### Revenue by category

<img width="616" height="424" alt="category" src="https://github.com/user-attachments/assets/fb346b3f-babf-4e1f-8c19-72c16cc79f90" />


Bikes make up **94.89%** of revenue. Accessories add 3.64% and clothing about 1.5%.

**So what:** the business depends on one product line. Accessories and clothing are natural add-ons for bike buyers and are barely used.

### Sales trend

<img width="940" height="424" alt="trend" src="https://github.com/user-attachments/assets/f78b9530-88cc-4a87-bae9-cb3767dd7c76" />


Monthly revenue hovered between about $0.3M and $0.7M through 2015 and early 2016. From August 2016 the line climbs steadily, reaching $1.6M in December 2016 and about $1.8M by June 2017.

**So what:** growth is recent and sharp, so the key planning question is what changed in mid-2016 and whether it can be repeated.

### Smart narrative

<img width="740" height="424" alt="narrative" src="https://github.com/user-attachments/assets/6e02bc50-6c07-4ecb-9073-b20d833b325b" />


Power BI's narrative visual writes the headline movements automatically and updates as filters change:

- Revenue grew **212.14%** from January 2015 to June 2017.
- From August 2016 it rose **127.18%** in ten months, from about $804K to $1.83M.
- Australia's revenue is far ahead of Central's, which is the lowest at about $3.1K.

---

## Key insights

- **Growth is accelerating.** Revenue more than tripled in 30 months, and a large share of that came in the last ten.
- **Margins are strong.** A profit margin near 42% leaves room to invest in marketing and returns reduction.
- **Three regions carry the business.** Australia, Southwest and Northwest account for about 61% of revenue.
- **One category dominates.** Bikes are almost 95% of sales, so a downturn in bikes would hit hard.
- **Professionals spend most.** Professional and Skilled Manual customers contribute over half of revenue.
- **Gender split is even.** No gender-based strategy is needed.

## Recommendations

1. **Protect and grow the top markets.** Prioritise inventory and campaigns in Australia and the two western US regions.
2. **Cross-sell accessories and clothing.** Bundle gear and apparel with bike purchases to reduce dependence on one category.
3. **Target high-value occupations.** Build offers for Professional and Skilled Manual customers, and test an entry range for Manual customers.
4. **Investigate the 1,828 returns.** Break returns down by product and region to find fixable causes.
5. **Audit the near-zero regions.** Confirm whether Southeast, Northeast and Central are real markets or missing data.

## Limitations and next steps

- Percentage comparisons against a near-zero base (such as Australia vs Central) say "Central is very small", not that Australia grew by that amount.
- The data ends in June 2017, so the latest month may be incomplete.
- Next: add year-on-year and profit-by-category views, break down returns, and add a forecast to the trend line.

---

## Repository contents

```
├── README.md
└── images/        dashboard screenshots used in this page
```

*(Add your `.pbix` file here if you want others to open the report.)*

## Author

**Seye Analytics** — [GitHub](https://github.com/SeyeAnalytics)
