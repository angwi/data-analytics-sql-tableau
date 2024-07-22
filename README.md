# Bike Sales Executive Dashboard
## The problem
The management of a bike sales company wants to know the conditions of sales activities within the company and gain insights into the various trends happening in the sales volume over the 2016, 2017 and 2018 periods. It also wants to know 
- the revenue per region, per store, per product category and per brand.
- a list of top customers
## Data Source
The data is found in the company's relational database; a Microsoft SQL Server. It was retrieved using SQL to create a dataset.
## SQL

```sql
SELECT 
	ord.order_id,
	CONCAT(cus.first_name, ' ', cus.last_name) AS 'customers',
	cus.city,
	cus.state,
	ord.order_date,
	SUM(oi.quantity) AS 'total_units',
	SUM(oi.quantity*oi.list_price) AS revenue,
	pd.product_name,
	cat.category_name,
	st.store_name,
	br.brand_name,
	CONCAT(stf.first_name, ' ', stf.last_name) AS 'sales_rep'
FROM sales.orders ord
JOIN sales.customers cus
ON ord.customer_id = cus.customer_id
JOIN sales.order_items oi
ON ord.order_id = oi.order_id
JOIN production.products pd
ON oi.product_id = pd.product_id
JOIN production.categories cat
ON pd.category_id = cat.category_id
JOIN sales.stores st
ON ord.store_id = st.store_id
JOIN production.brands br
ON pd.brand_id = br.brand_id
JOIN sales.staffs stf
ON ord.staff_id = stf.staff_id
GROUP  BY 
	ord.order_id,
	CONCAT(cus.first_name, ' ', cus.last_name),
	cus.city,
	cus.state,
	ord.order_date,
	pd.product_name,
	cat.category_name,
	st.store_name,
	br.brand_name,
	CONCAT(stf.first_name, ' ', stf.last_name)
```
<p>
	The dataset was saved as csv file and then imported into Tableau public to create a dashboard.
</p>

## Dashboard
<p />
<a href ="https://public.tableau.com/app/profile/dominic.eyinembi.ncho/viz/bike-sales-final/Dashboard1?publish=yes" target="_blank">Click this link to interact with the Dashboard</a>
<p>Part of the dashboard is shown below:</p>
<img src="https://github.com/angwi/data-analytics-sql-tableau/blob/main/dashboard-part.PNG" alt="Part dashboard" />
