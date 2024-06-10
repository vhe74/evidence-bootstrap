---
title : Marketing channels
---

### Sales evolution
<Dropdown data={categories} name=category value=category>
    <DropdownOption value="%" valueLabel="All Categories"/>
</Dropdown>

<Dropdown data={years} name=year value=year>
    <DropdownOption value="%" valueLabel="All Years"/>
</Dropdown>

<Dropdown data={channels} name=channel value=channel>
    <DropdownOption value="%" valueLabel="All Channels"/>
</Dropdown>

<BarChart 
    data={sales}
    x=order_month
    y=sales
    series=channel
/>






<hr/>
<Details title='Queries'>

```sql channels_data
SELECT 
category,
state,
channel,
channel_month,
order_month,
sum(sales) sales
FROM needful_things.orders
GROUP BY ALL
```

```sql channels
SELECT DISTINCT(channel)
FROM ${channels_data}
```

```sql categories
SELECT DISTINCT(category)
FROM ${channels_data}
```

```sql states
SELECT DISTINCT(state)
FROM ${channels_data}
```

```sql years
SELECT DISTINCT(CAST( EXTRACT('year' FROM order_month) AS VARCHAR) ) AS year
FROM ${channels_data}
```

```sql sales
SELECT 
    order_month,
    sum(sales) as sales,
    category,
    channel
FROM ${channels_data}
WHERE category like '${inputs.category.value}'
 AND date_part('year', order_month) like '${inputs.year.value}'
 AND channel like '${inputs.channel.value}'
GROUP BY ALL
ORDER BY sales DESC
```


</Details>

