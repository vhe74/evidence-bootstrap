---
title: Ventes de produits
---

Cette page détaille des statistiques de ventes de produits


## Categories

<BarChart
  data={categories}
  x=category
  y=sales_usd
  swapXY=true
/>

## Evolution des ventes 
<LineChart
  data={sales_by_date}
  x=order_month
  y=sales
/>

<BarChart
  data={sales_by_date_with_cat}
  x=order_month
  y=sales
  series=category
/>









```sql categories
  select
      category, sum(sales) as sales_usd,
  from needful_things.orders
  group by category
  order by sales_usd DESC
```

```sql sales_by_date
  select
    order_month, 
    --category, 
    sum(sales) sales,
  from needful_things.orders
  group by order_month --, category
  order by order_month ASC
```

```sql sales_by_date_with_cat
  select
    order_month, 
    category, 
    sum(sales) sales,
  from needful_things.orders
  group by order_month , category
  order by order_month ASC
```
