---
title : Categories de produits
---

<DataTable
    data={categories}
    link=category_link
/>


```sql categories 
SELECT 
category, 
COUNT(*) AS "Nombre de ventes", 
'/categories/' || category as category_link
FROM needful_things.orders
GROUP BY category
```