# shipments-mock-data-
An end-to-end Power BI project analyzing a mock e-commerce/logistics shipment dataset, focused on delivery performance, on-time rate, carrier/warehouse efficiency, and failure-reason analysis. The dataset was deliberately generated with realistic data-quality issues (inconsistent text casing, typos, mixed date formats, stray whitespace, and outlier values) to demonstrate a full data-cleaning and modeling workflow before visualization.

📊 Project Overview
Domain: E-commerce logistics / last-mile delivery
Goal: Measure and explain shipment delivery performance — on-time rate, delivery outcomes (Delivered / Returned / Cancelled / Failed / In Transit), and the key drivers behind failed or late deliveries — across carriers, warehouses, origin/destination countries, and product categories.
Tool: Microsoft Power BI Desktop (data modeling, DAX measures, and report visuals)
Data: 1,225 mock shipment records, single fact table shipment_mock_data.


🗂️ Repository Contents
File	Description
SHIPMENT_MOCK_DATA.pbix	Power BI Desktop file — data model, DAX measures, and the full report
shipments_mock_dataset.csv	Raw source dataset (intentionally "dirty" for cleaning practice)
README.md	Project documentation.


🧾 Dataset Schema
Column	Description
order_id	Unique shipment identifier
order_date	Date the order was placed (mixed formats in raw data)
origin_country	Country the shipment originated from
destination_country	Destination country
carrier	Shipping carrier (e.g., Aramex, DHL, SMSA, FastCourier, Local Fleet)
warehouse	Fulfillment warehouse code (e.g., AMM-WH1, DXB-WH1, IST-WH1)
product_category	Product category (Electronics, Fashion, Books, etc.)
weight_kg	Package weight in kilograms
shipping_cost_usd	Shipping cost in USD
cod_amount_usd	Cash-on-delivery amount, where applicable
status	Shipment status (Delivered, Returned, Cancelled, Failed Delivery, In Transit)
delivery_date	Actual delivery timestamp
sla_days_target	Target SLA (days) for delivery
fail_reason	Reason for failure, where applicable (e.g., Customs Delay, Damaged Package)


🧹 Data Cleaning Challenges Addressed

The raw CSV was designed to mimic real-world messy operational data, including:

Inconsistent categorical values: e.g., carrier appearing as Aramex / aramex; status appearing as Delivered / DELIVERED / Deliverd / delivered; country names as UAE / U.A.E., Saudi Arabia / KSA
Stray whitespace: category values such as "  Electronics  " with leading/trailing spaces
Mixed date formats: order_date stored inconsistently as DD/MM/YYYY, MM-DD-YYYY, and YYYY-MM-DD [HH:MM] within the same column
Missing values: ~9% of records missing a delivery_date; blank carrier and product_category entries
Invalid/outlier numeric values: negative shipping_cost_usd and weight_kg entries; extreme outliers (weights up to 1,500 kg)
Duplicate concept fields: overlapping status labels needing standardization into a single clean category set before analysis

These issues were standardized in Power Query / the data model prior to building measures and visuals, so the DAX layer operates on clean, consistent columns (e.g., a normalized status, a computed shipping days and is on time flag).

📈 Dashboard Structure

Page 1 — Delivery Performance Overview

KPI card: On-Time Rate
Key Influencers visual explaining what drives on-time delivery, based on carrier, warehouse, origin/destination country, product category, SLA target, and shipment weight
Bar chart: average shipping cost by product category
Column chart: shipment count by failure reason

Page 2 — Delivery Decomposition

Decomposition tree breaking down Delivered Orders by destination country, product category, shipping days, origin country, carrier, warehouse, and COD amount — for root-cause and drill-down analysis.




🔑 Key Measures
On-Time Rate — share of shipments delivered within their SLA target
Delivered Orders — count of successfully delivered shipments
is on time (flag) — whether an individual shipment met its sla_days_target
shipping days — actual days elapsed between order date and delivery date




🚀 How to Use
Download SHIPMENT_MOCK_DATA.pbix and open it in Power BI Desktop.
The data source path may need to be repointed to shipments_mock_dataset.csv on your machine (Home → Transform Data → Data Source Settings).
Refresh the data model to load the report.

Note: This dataset is synthetic/mock data created for portfolio and learning purposes; it does not represent real company shipment records.
