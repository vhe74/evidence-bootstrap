---
title : Sales Explorer
---

### Sales evolution

<DimensionGrid 
    data={salesDim} 
    name="selected_dimensions"
    metric=sum(sales)
/>

<BarChart 
    data={sales}
    x=order_month
    y=sales
    series=channel
/>

<hr/>
<Details title='Queries'>

```sql all_data
SELECT 
    category,
    state,
    channel,
    channel_month,
    order_month,
    state,
    CAST( EXTRACT('year' FROM order_month) AS VARCHAR) AS year,
    sum(sales) sales
FROM needful_things.orders
GROUP BY ALL
```

```sql salesDim 
SELECT 
    order_month,
    category,
    channel,
    state,
    year,
    sum(sales) as sales,
FROM ${all_data}
GROUP BY ALL
```

```sql sales
SELECT 
    order_month,
    category,
    channel,
    state,
    year,
    sum(sales) as sales,
FROM ${all_data}
WHERE ${inputs.selected_dimensions}
GROUP BY ALL
ORDER BY sales DESC
```


</Details>

