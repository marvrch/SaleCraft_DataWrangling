# SaleCraft — My Data Wrangling Project

## Background Problem

This project explores a real online retail dataset to practice the core steps of data work, with a strong emphasis on making messy data trustworthy. The raw file contains common issues such as duplicated lines, inconsistent product codes, missing customers, and mixed invoice types that include cancellations and adjustments.
The goal is to turn this raw file into three usable views:

* **all\_data**: the auditable source with quality flags
* **cleaned\_data**: rows that represent real sales only
* **fe\_data**: a model friendly table with simple features

The notebook documents each step so readers can trace how raw transactions become consistent and easy to analyze.

## Tools & Libraries

* **Python**
* **Pandas** and **NumPy** for wrangling
* Built in **Pandas get\_dummies** for one hot encoding

## Insights

The analysis focuses on data quality first, then simple feature building. These are the key takeaways that I found:

* **Most orders come from the United Kingdom.** International lines are present but much smaller in volume.
* **Not every row is a purchase.** Many negative quantities belong to credit notes and adjustments. After filtering to numeric invoices with positive quantity and price, the table reflects actual sales more reliably.
* **Product codes needed careful handling.** Numeric codes and codes with short letter tails often represent real SKUs, while known service codes such as POST or DOT are not SKUs. Two families that look like services, **DCGSSGIRL** and **DCGSSBOY**, were treated as valid SKUs by exception.
* **Descriptions were standardized.** For each StockCode, the most frequent description was used, which removes small text variations and fills missing values.
* **Baskets are multi item.** Many invoices contain several lines and several unique SKUs. Simple aggregates like invoice total value, number of items, number of lines, and number of SKUs capture basket size in a compact way.
* **A reliable core was retained.** After cleaning, the project works with about **three hundred and fifty eight thousand** sales lines that are consistent and ready for downstream work.

You can explore the full workflow in the accompanying notebook to see how each flag and filter changes the data.

## Advices

This project intentionally keeps feature work simple. If you want to take it further, consider focusing on **data transformation**:

* Add richer encodings for high cardinality fields, for example target encoding for categories with many values.
* Create time based features beyond year and month, such as week number, holiday markers, and moving window aggregates.
* Normalize or standardize numeric features when models require it.
* Engineer product level attributes, for example price bands and lifetime revenue per SKU.
* Turn the steps into a reproducible pipeline so cleaning and transformation run the same way every time.

These extensions will deepen skills in making inconsistent data consistent and will provide hands on practice with practical data transformation.
