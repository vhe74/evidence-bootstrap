# Catégorie : "{params.category}"




<Value data={distinct_products_count} /> produits différents
<br/>
<Value data={distinct_customers_count} /> clients différents

<Grid cols=2>
<BarChart
    title="TOP channels"
    data={Top_channels}
    x=channel
    y=sales
    swapXY=true
/>
<BarChart
    title="TOP states"
    data={Top_states}
    x=state
    y=sales
    swapXY=true
/>
</Grid>

<DataTable data={all_sales_by_cat}/>




<Details title='Queries'>

```sql all_sales_by_cat
SELECT 
item,
category,
state,
channel,
order_month,
first_name || ' ' || last_name as customer,
sales
FROM needful_things.orders
WHERE category = '${params.category}'
```

```sql distinct_products_count
SELECT COUNT(DISTINCT(item))
FROM ${all_sales_by_cat}
```
```sql distinct_customers_count
SELECT COUNT(DISTINCT(customer))
FROM ${all_sales_by_cat}
```

```sql Top_channels
SELECT channel, sum(sales) sales
FROM ${all_sales_by_cat}
GROUP BY channel
ORDER BY sales DESC
LIMIT 10
```

```sql Top_states
SELECT state, sum(sales) sales
FROM ${all_sales_by_cat}
GROUP BY state
ORDER BY sales DESC
LIMIT 10
```
</Details>

