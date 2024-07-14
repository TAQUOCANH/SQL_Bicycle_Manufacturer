# SQL_Bicycle_Manufacturer
## Dataset
<p>Dataset: adventureworks2019 (public Google BigQuery dataset)</p>
<p>Dataset dictionary: Please reach file "Data Dictionary" attached above</p>
<p></p>Dataset Schema:  https://i0.wp.com/improveandrepeat.com/wp-content/uploads/2018/12/AdvWorksOLTPSchemaVisio.png?ssl=1</p>
<p>Dataset access:
  <ul>
  <li>Log in to your Google Cloud Platform account and create a new project.</li>
  <li>Navigate to the BigQuery console and select your newly created project.</li>
  <li>In the navigation panel, select "Add Data" and then "Star a project by name".</li>
  <liEnter the project name "adventurework2019"></li>
</ul>
    
### Query 1: Calculate Quantity of items, Sales value & Order quantity by each Subcategory in L12M
```sql
SELECT 
       FORMAT_DATETIME("%b %Y", sales_tbl.ModifiedDate) period
       ,sub_tbl.Name
       ,SUM(sales_tbl.OrderQty) qty_item
       ,SUM(sales_tbl.LineTotal) total_sales
       ,COUNT(DISTINCT sales_tbl.SalesOrderID) order_cnt
FROM `adventureworks2019.Sales.SalesOrderDetail` sales_tbl
LEFT JOIN `adventureworks2019.Production.Product` product_tbl
  ON sales_tbl.ProductID = product_tbl.ProductID
LEFT JOIN `adventureworks2019.Production.ProductSubcategory` sub_tbl
  ON CAST(product_tbl.ProductSubcategoryID AS INT) = sub_tbl.ProductSubcategoryID 
WHERE sales_tbl.ModifiedDate >= TIMESTAMP(DATE_ADD(DATE((SELECT MAX(ModifiedDate) FROM `adventureworks2019.Sales.SalesOrderDetail`)), INTERVAL -12 MONTH))
GROUP BY 1,2
ORDER BY 1 DESC,2 ;
```

| period    | Name                | qty_item | total_sales          | order_cnt |
|-----------|---------------------|----------|----------------------|-----------|
| Sep 2013  | Bike Racks          | 312      | 22828.512000000002   | 71        |
| Sep 2013  | Bike Stands         | 26       | 4134.0               | 26        |
| Sep 2013  | Bottles and Cages   | 803      | 4676.56280799994     | 380       |
| Sep 2013  | Bottom Brackets     | 60       | 3118.1400000000008   | 19        |
| Sep 2013  | Brakes              | 100      | 6390.0               | 29        |
| Sep 2013  | Caps                | 440      | 2879.4826160000002   | 203       |
| Sep 2013  | Chains              | 62       | 752.92800000000022   | 24        |
| Sep 2013  | Cleaners            | 296      | 1611.8307000000029   | 108       |
| Sep 2013  | Cranksets           | 75       | 13955.85             | 20        |
| Sep 2013  | Derailleurs         | 97       | 5972.069999999997    | 23        |
| Sep 2013  | Fenders             | 169      | 3714.6200000000026   | 169       |
| Sep 2013  | Gloves              | 444      | 7552.24579199999     | 146       |
| Sep 2013  | Handlebars          | 131      | 6486.5880000000016   | 47        |
| Sep 2013  | Helmets             | 1016     | 27354.835599000184   | 480       |
| Sep 2013  | Hydration Packs     | 249      | 9186.1619849999934   | 87        |
| Sep 2013  | Jerseys             | 1402     | 48318.089182         | 304       |
| Sep 2013  | Locks               | 1        | 15.0                 | 1         |
| Sep 2013  | Mountain Bikes      | 1194     | 1244716.8356249924   | 263       |
| Sep 2013  | Mountain Frames     | 662      | 224303.9760000002    | 34        |
| Sep 2013  | Pedals              | 438      | 16565.111999999986   | 76        |
| Sep 2013  | Road Bikes          | 1398     | 1318888.686874995    | 319       |
| Sep 2013  | Road Frames         | 264      | 110277.03599999998   | 38        |
| Sep 2013  | Saddles             | 170      | 4250.052             | 39        |
| Sep 2013  | Shorts              | 713      | 30568.71341700001    | 130       |
| Sep 2013  | Socks               | 430      | 2438.9627270000005   | 88        |
| Sep 2013  | Tights              | 5        | 243.71749999999997   | 1         |
| Sep 2013  | Tires and Tubes     | 1420     | 18561.387999999981   | 787       |
| Sep 2013  | Touring Bikes       | 1238     | 1214628.9048989993   | 171       |
| Sep 2013  | Touring Frames      | 337      | 154334.6393279999    | 21        |
| Sep 2013  | Vests               | 623      | 24100.466150000007   | 102       |
| Sep 2013  | Wheels              | 1        | 83.2981              | 1         |
| Oct 2013  | Bike Racks          | 284      | 21181.2              | 70        |
| Oct 2013  | Bike Stands         | 24       | 3816.0               | 24        |
| Oct 2013  | Bottles and Cages   | 845      | 5038.95319199993     | 400       |
| Oct 2013  | Bottom Brackets     | 132      | 7030.0080000000025   | 30        |
| Oct 2013  | Brakes              | 142      | 9036.7806000000037   | 38        |
| Oct 2013  | Caps                | 406      | 2738.8412579999995   | 208       |
| Oct 2013  | Chains              | 93       | 1122.3565760000004   | 31        |
| Oct 2013  | Cleaners            | 294      | 1612.7560800000033   | 108       |
| Oct 2013  | Cranksets           | 118      | 19722.792            | 33        |
| Oct 2013  | Derailleurs         | 135      | 8291.8079999999918   | 35        |
| Oct 2013  | Fenders             | 170      | 3736.6000000000026   | 170       |
| Oct 2013  | Gloves              | 447      | 7678.8126749999883   | 148       |
| Oct 2013  | Handlebars          | 188      | 9196.1039999999975   | 56        |
| Oct 2013  | Helmets             | 1127     | 30733.9913500002     | 557       |
| Oct 2013  | Hydration Packs     | 243      | 9207.6135839999934   | 86        |
| Oct 2013  | Jerseys             | 1372     | 47761.25915300005    | 324       |
| Oct 2013  | Mountain Bikes      | 1231     | 1338738.67399999     | 305       |
| Oct 2013  | Mountain Frames     | 632      | 221830.44582800008   | 32        |
| Oct 2013  | Pedals              | 374      | 14060.975999999986   | 72        |
| Oct 2013  | Road Bikes          | 1288     | 1217739.1194059956   | 363       |
| Oct 2013  | Road Frames         | 247      | 99189.749999999913   | 40        |
| Oct 2013  | Saddles             | 226      | 5991.3741119999977   | 56        |
| Oct 2013  | Shorts              | 661      | 28533.348225000045   | 122       |
| Oct 2013  | Socks               | 358      | 2076.2611770000017   | 86        |
| Oct 2013  | Tires and Tubes     | 1531     | 21152.65599999989    | 849       |
| Oct 2013  | Touring Bikes       | 1522     | 1497460.966236       | 221       |
| Oct 2013  | Touring Frames      | 283      | 137878.104           | 28        |
| Oct 2013  | Vests               | 611      | 23255.738350000003   | 93        |
| Nov 2013  | Bike Racks          | 142      | 11472.0              | 50        |
| Nov 2013  | Bike Stands         | 24       | 3816.0               | 24        |
| Nov 2013  | Bottles and Cages   | 894      | 5883.5719999999092   | 482       |
| Nov 2013  | Bottom Brackets     | 24       | 1749.4560000000001   | 9         |
| Nov 2013  | Brakes              | 26       | 1661.3999999999999   | 8         |
| Nov 2013  | Caps                | 319      | 2429.2849920000008   | 221       |
| Nov 2013  | Chains              | 24       | 291.456              | 9         |
| Nov 2013  | Cleaners            | 202      | 1230.6600000000039   | 111       |
| Nov 2013  | Cranksets           | 32       | 6949.608             | 10        |
| Nov 2013  | Derailleurs         | 35       | 1921.29              | 11        |
| Nov 2013  | Fenders             | 165      | 3625.500000000002    | 165       |
| Nov 2013  | Gloves              | 410      | 7107.297000000006    | 142       |
| Nov 2013  | Handlebars          | 59       | 2970.0               | 20        |
| Nov 2013  | Helmets             | 943      | 25348.524            | 446       |
| Nov 2013  | Hydration Packs     | 181      | 6841.952000000002    | 80        |
| Nov 2013  | Jerseys             | 1191     | 41398.737            | 294       |
| Nov 2013  | Mountain Bikes      | 1313     | 1429615.2211999998   | 352       |
| Nov 2013  | Mountain Frames     | 398      | 138965.14599999999   | 22        |
| Nov 2013  | Pedals              | 242      | 9310.319999999996    | 60        |
| Nov 2013  | Road Bikes          | 1287     | 1216267.087000001    | 369       |
| Nov 2013  | Road Frames         | 154      | 61852.0              | 30        |
| Nov 2013  | Saddles             | 129      | 3408.088             | 36        |
| Nov 2013  | Shorts              | 450      | 19424.04             | 92        |
| Nov 2013  | Socks               | 290      | 1692.8531999999994   | 67        |
| Nov 2013  | Tights              | 7        | 341.20499999999998   | 3         |
| Nov 2013  | Tires and Tubes     | 1510     | 20875.968            | 859       |
| Nov 2013  | Touring Bikes       | 1425     | 1402112.4451         | 206       |
| Nov 2013  | Touring Frames      | 201      | 97858.8952           | 13        |
| Nov 2013  | Vests               | 451      | 17161.557            | 69        |

### Query 2: Calculate % YoY growth rate by SubCategory & release top 3 cat with highest grow rate. Can use metric: quantity_item. Round results to 2 decimal

```sql
WITH
qty_per_year AS(
  SELECT 
       sub_tbl.Name Name
       ,EXTRACT(YEAR FROM sales_tbl.ModifiedDate) year
       ,SUM(sales_tbl.OrderQty) qty_item
  FROM `adventureworks2019.Sales.SalesOrderDetail` sales_tbl
  LEFT JOIN `adventureworks2019.Production.Product` product_tbl
    ON sales_tbl.ProductID = product_tbl.ProductID
  LEFT JOIN `adventureworks2019.Production.ProductSubcategory` sub_tbl
    ON CAST(product_tbl.ProductSubcategoryID AS INT) = sub_tbl.ProductSubcategoryID 
  GROUP BY 1,2
  ORDER  BY 1,2
)
, add_previ_qty_year AS(
  SELECT 
       Name
       ,year
       ,qty_item
       ,LEAD(qty_item) OVER(PARTITION BY Name ORDER BY year DESC) prv_qty
  FROM qty_per_year
)
, yoy_sale AS(
  SELECT
      Name
      ,qty_item
      ,prv_qty
      ,ROUND((qty_item-prv_qty)*1.0/prv_qty, 2) qty_diff
  FROM add_previ_qty_year
  ORDER BY 4 DESC
)
, rank_yoy_sale AS (
  SELECT
      *
      , DENSE_RANK() OVER(ORDER BY qty_diff DESC) rank_yoy
  FROM yoy_sale
)

SELECT
  Name
  ,qty_item
  ,prv_qty
  ,qty_diff
FROM rank_yoy_sale
WHERE rank_yoy <= 3
ORDER BY rank_yoy;
```

| Name             | qty_item | prv_qty | qty_diff |
|------------------|----------|---------|----------|
| Mountain Frames  | 3168     | 510     | 5.21     |
| Socks            | 2724     | 523     | 4.21     |
| Road Frames      | 5564     | 1137    | 3.89     |

### Query 3: Ranking Top 3 TeritoryID with biggest Order quantity of every year. If there's TerritoryID with same quantity in a year, do not skip the rank number

```sql
WITH
qty_of_terri_per_yr AS (
  SELECT
       EXTRACT(YEAR FROM sales_tbl.ModifiedDate) yr
       ,TerritoryID
       ,SUM(sales_tbl.OrderQty) order_cnt
  FROM `adventureworks2019.Sales.SalesOrderDetail` sales_tbl
  LEFT JOIN `adventureworks2019.Sales.SalesOrderHeader` sales_header
    ON sales_tbl.SalesOrderID = sales_header.SalesOrderID
  GROUP BY 1, 2
  ORDER BY 1 DESC, 3 DESC
)
,terri_rank AS(
  SELECT
        yr
        ,TerritoryID
        ,order_cnt
        ,DENSE_RANK() OVER(PARTITION BY yr ORDER BY order_cnt DESC) rk
  FROM qty_of_terri_per_yr
)

SELECT *
FROM terri_rank
WHERE rk <= 3
ORDER BY 1 DESC, 4 ;
```

| yr   | TerritoryID | order_cnt | rk |
|------|-------------|-----------|----|
| 2014 | 4           | 11632     | 1  |
| 2014 | 6           | 9711      | 2  |
| 2014 | 1           | 8823      | 3  |
| 2013 | 4           | 26682     | 1  |
| 2013 | 6           | 22553     | 2  |
| 2013 | 1           | 17452     | 3  |
| 2012 | 4           | 17553     | 1  |
| 2012 | 6           | 14412     | 2  |
| 2012 | 1           | 8537      | 3  |
| 2011 | 4           | 3238      | 1  |
| 2011 | 6           | 2705      | 2  |
| 2011 | 1           | 1964      | 3  |


<ul>

<li>TerritoryID 4 consistently leads in the number of orders from 2011 to 2014.</li>
<li>TerritoryID 6 consistently ranks second each year, indicating this is also a region with stable sales.</li>
<li>TerritoryID 1 ranks third in all years, consistently ranking despite fluctuations in the number of orders.</li>
</ul>

### Query 4: Calculate Total Discount Cost belongs to Seasonal Discount for each SubCategory

```sql
WITH discount_cost_raw AS(
SELECT 
       sales_tbl.*
       ,sub_tbl.Name Name
       ,special_offer.DiscountPct
       ,special_offer.Type
       ,special_offer.DiscountPct * sales_tbl.OrderQty * sales_tbl.UnitPrice disc_cost
FROM `adventureworks2019.Sales.SalesOrderDetail` sales_tbl
LEFT JOIN `adventureworks2019.Production.Product` product_tbl
    ON sales_tbl.ProductID = product_tbl.ProductID
LEFT JOIN `adventureworks2019.Production.ProductSubcategory` sub_tbl
    ON CAST(product_tbl.ProductSubcategoryID AS INT) = sub_tbl.ProductSubcategoryID
LEFT JOIN `adventureworks2019.Sales.SpecialOffer` special_offer
    ON sales_tbl.SpecialOfferID = special_offer.SpecialOfferID 
WHERE LOWER(special_offer.Type) LIKE '%seasonal discount%'
)

SELECT 
    FORMAT_TIMESTAMP("%Y", discount_cost_raw.ModifiedDate)
    , Name
    , sum(disc_cost) as total_cost
    
FROM discount_cost_raw
GROUP BY 1,2
;
```


| f0_ | Name    | total_cost     |
|-----|---------|----------------|
| 2012 | Helmets | 827.64732      |
| 2013 | Helmets | 1606.041       |


### Query 5: Retention rate of Customer in 2014 with status of Successfully Shipped (Cohort Analysis)

```sql
WITH
cus_info AS (
  SELECT 
        EXTRACT(YEAR FROM ModifiedDate) yr
        ,EXTRACT(MONTH FROM ModifiedDate) month
        ,CustomerID
        ,COUNT(DISTINCT SalesOrderID) sale_cnt
  FROM `adventureworks2019.Sales.SalesOrderHeader`
  WHERE Status = 5 AND EXTRACT(YEAR FROM ModifiedDate) = 2014
  GROUP BY 1,2,3
)
,row_num AS (
  SELECT *
         ,ROW_NUMBER() OVER(PARTITION BY CustomerID ORDER BY month) row_nb
  FROM cus_info
)
,first_order AS(
  SELECT
        month first_month
        ,yr
        ,CustomerID
  FROM row_num
  WHERE row_nb = 1
)
,join_all_and_month_diff AS (
  SELECT
        cus.month
        ,cus.yr
        ,cus.CustomerID
        ,f_o.first_month
        ,CONCAT('M',' - ' ,cus.month - f_o.first_month) month_diff
  FROM cus_info cus
  LEFT JOIN first_order f_o
    ON cus.CustomerID = f_o.CustomerID
)
, cohort_raw_data AS(
SELECT
      first_month as month_join
      ,month_diff
      ,COUNT(DISTINCT CustomerID) customer_cnt
FROM join_all_and_month_diff
GROUP BY 1, 2
ORDER BY 1, 2 
)

SELECT 
    month_join,
    SUM(CASE WHEN month_diff = 'M - 0' THEN customer_cnt ELSE 0 END) AS M_0,
    SUM(CASE WHEN month_diff = 'M - 1' THEN customer_cnt ELSE 0 END) AS M_1,
    SUM(CASE WHEN month_diff = 'M - 2' THEN customer_cnt ELSE 0 END) AS M_2,
    SUM(CASE WHEN month_diff = 'M - 3' THEN customer_cnt ELSE 0 END) AS M_3,
    SUM(CASE WHEN month_diff = 'M - 4' THEN customer_cnt ELSE 0 END) AS M_4,
    SUM(CASE WHEN month_diff = 'M - 5' THEN customer_cnt ELSE 0 END) AS M_5,
    SUM(CASE WHEN month_diff = 'M - 6' THEN customer_cnt ELSE 0 END) AS M_6
FROM cohort_raw_data
GROUP BY month_join
ORDER BY month_join
;
```

| month_join | M_0 | M_1 | M_2 | M_3 | M_4 | M_5 | M_6 |
|------------|-----|-----|-----|-----|-----|-----|-----|
| 1          | 2076| 78  | 89  | 252 | 96  | 61  | 18  |
| 2          | 1805| 51  | 61  | 234 | 58  | 8   | 0   |
| 3          | 1918| 43  | 58  | 44  | 11  | 0   | 0   |
| 4          | 1906| 34  | 44  | 7   | 0   | 0   | 0   |
| 5          | 1947| 40  | 7   | 0   | 0   | 0   | 0   |
| 6          | 909 | 10  | 0   | 0   | 0   | 0   | 0   |
| 7          | 148 | 0   | 0   | 0   | 0   | 0   | 0   |

- **Sharp decline from the first month (M-0) to the second month (M-1):** This is the most significant drop across all cohorts, indicating that customers do not remain active for long after joining.
- **Very low customer retention rate:** The retention rate for all cohorts is very low. Strategies to improve retention rates after the first month are needed to enhance customer engagement.


### Query 6: Trend of Stock level & MoM diff % by all product in 2011. If %gr rate is null then 0. Round to 1 decimal

```sql
WITH
month_fg AS (
  SELECT 
        b.Name Name
        ,EXTRACT(MONTH FROM a.ModifiedDate) mth
        ,EXTRACT(YEAR FROM a.ModifiedDate) yr
        ,SUM(a.StockedQty) stock_qty
  FROM `adventureworks2019.Production.WorkOrder` a
  LEFT JOIN `adventureworks2019.Production.Product` b
    ON a.ProductID = b.ProductID
  WHERE EXTRACT(YEAR FROM a.ModifiedDate) = 2011
  GROUP BY 1, 2, 3
  ORDER BY 1, 2 DESC
)
,mom_fg AS (
  SELECT
        *
        ,LEAD(stock_qty,1) OVER(PARTITION BY Name ORDER BY yr, mth DESC) stock_prv
  FROM month_fg
)

SELECT
      *
      ,IFNULL(ROUND((stock_qty-stock_prv)*100.0 / stock_prv,1),0) diff
FROM mom_fg
ORDER BY 1, 2 DESC ;
```


| Row | Name           | mth | yr   | stock_qty | stock_prv | diff  |
|-----|----------------|-----|------|-----------|-----------|-------|
| 1   | BB Ball Bearing| 12  | 2011 | 8,475     | 14,544    | -41.7 |
| 2   | BB Ball Bearing| 11  | 2011 | 14,544    | 19,175    | -24.2 |
| 3   | BB Ball Bearing| 10  | 2011 | 19,175    | 8,845     | 116.8 |
| 4   | BB Ball Bearing| 9   | 2011 | 8,845     | 9,666     | -8.5  |
| 5   | BB Ball Bearing| 8   | 2011 | 9,666     | 12,837    | -24.7 |
| 6   | BB Ball Bearing| 7   | 2011 | 12,837    | 5,259     | 144.1 |
| 7   | BB Ball Bearing| 6   | 2011 | 5,259     | null      | 0.0   |
| 8   | Blade          | 12  | 2011 | 1,842     | 3,598     | -48.8 |
| 9   | Blade          | 11  | 2011 | 3,598     | 4,670     | -23.0 |
| 10  | Blade          | 10  | 2011 | 4,670     | 2,122     | 120.1 |
| 11  | Blade          | 9   | 2011 | 2,122     | 2,382     | -10.9 |
| 12  | Blade          | 8   | 2011 | 2,382     | 3,166     | -24.8 |
| 13  | Blade          | 7   | 2011 | 3,166     | 1,280     | 147.3 |
| 14  | Blade          | 6   | 2011 | 1,280     | null      | 0.0   |
| ...  | ...          | ..   | ... | ...     | ...      | ...   |

### Query 7: Calc Ratio of Stock / Sales in 2011 by product name, by month .Order results by month desc, ratio desc. Round Ratio to 1 decimal mom yoy

```sql
WITH
sale_data AS(
    SELECT 
        EXTRACT(MONTH FROM sales_tbl.ModifiedDate) month
        ,EXTRACT(YEAR FROM sales_tbl.ModifiedDate) year
        ,sales_tbl.ProductID
        ,product_tbl.Name Name
        ,COALESCE(SUM(sales_tbl.OrderQty),0) sale
       --,IFNULL(SUM(workorder_tbl.StockedQty),0) stock
       --,ROUND(SUM(workorder_tbl.StockedQty) *1.0 / SUM(sales_tbl.OrderQty), 1) ratio
    FROM `adventureworks2019.Sales.SalesOrderDetail` sales_tbl
    LEFT JOIN `adventureworks2019.Production.Product` product_tbl
        ON sales_tbl.ProductID = product_tbl.ProductID
  --LEFT JOIN `adventureworks2019.Production.WorkOrder` workorder_tbl
      --ON sales_tbl.ProductID = workorder_tbl.ProductID
    WHERE EXTRACT(YEAR FROM sales_tbl.ModifiedDate) = 2011 
    GROUP BY 1, 2, 3, 4
    ORDER BY 1 DESC, 5 --, 7 DESC
)
,stock_data AS(
    SELECT
            workorder_tbl.ProductID
            ,EXTRACT(MONTH FROM workorder_tbl.ModifiedDate) month
            ,EXTRACT(YEAR FROM workorder_tbl.ModifiedDate) year
            ,COALESCE(SUM(workorder_tbl.StockedQty), 0) stock
    FROM `adventureworks2019.Production.WorkOrder` workorder_tbl
    WHERE EXTRACT(YEAR FROM workorder_tbl.ModifiedDate) = 2011
    GROUP BY 1,2,3
)

SELECT
    sale_data.month
    ,sale_data.year
    ,sale_data.ProductID
    ,sale_data.Name
    ,sale
    ,stock
    , ROUND((stock * 1.0) / sale, 1) ratio
FROM sale_data
FULL JOIN stock_data
ON sale_data.ProductID = stock_data.ProductID AND sale_data.month = stock_data.month AND sale_data.year = stock_data.year
ORDER BY 1 DESC, 7 DESC ;
```

| Row | month | year | ProductID | Name                             | sale | stock | ratio |
|-----|-------|------|-----------|----------------------------------|------|-------|-------|
| 1   | 12    | 2011 | 745       | HL Mountain Frame - Black, 48    | 1    | 27    | 27.0  |
| 2   | 12    | 2011 | 743       | HL Mountain Frame - Black, 42    | 1    | 26    | 26.0  |
| 3   | 12    | 2011 | 748       | HL Mountain Frame - Silver, 38   | 2    | 32    | 16.0  |
| 4   | 12    | 2011 | 722       | LL Road Frame - Black, 58        | 4    | 47    | 11.8  |
| 5   | 12    | 2011 | 747       | HL Mountain Frame - Black, 38    | 3    | 31    | 10.3  |
| 6   | 12    | 2011 | 726       | LL Road Frame - Red, 48          | 5    | 36    | 7.2   |
| 7   | 12    | 2011 | 738       | LL Road Frame - Black, 52        | 10   | 64    | 6.4   |
| 8   | 12    | 2011 | 730       | LL Road Frame - Red, 62          | 7    | 38    | 5.4   |
| 9   | 12    | 2011 | 741       | HL Mountain Frame - Silver, 48   | 5    | 27    | 5.4   |
| 10  | 12    | 2011 | 725       | LL Road Frame - Red, 44          | 12   | 53    | 4.4   |
| 11  | 12    | 2011 | 729       | LL Road Frame - Red, 60          | 10   | 43    | 4.3   |
| 12  | 12    | 2011 | 732       | ML Road Frame - Red, 48          | 10   | 16    | 1.6   |
| 13  | 12    | 2011 | 750       | Road-150 Red, 44                 | 25   | 38    | 1.5   |
| 14  | 12    | 2011 | 751       | Road-150 Red, 48                 | 32   | 47    | 1.5   |
| 15  | 12    | 2011 | 775       | Mountain-100 Black, 38           | 23   | 28    | 1.2   |
| 16  | 12    | 2011 | 773       | Mountain-100 Silver, 44          | 32   | 36    | 1.1   |
| 17  | 12    | 2011 | 752       | Road-150 Red, 52                 | 32   | 35    | 1.1   |
| 18  | 12    | 2011 | 765       | Road-650 Black, 58               | 39   | 43    | 1.1   |
| ...  | ...    | ... | ...       | ...               | ...   | ...    | ...   |


### Query 8: No of order and value at Pending status in 2014

```sql
SELECT  
        EXTRACT(YEAR FROM po_header.ModifiedDate) year
        ,Status
        ,COUNT(PurchaseOrderID) order_cnt
        ,SUM(TotalDue) value
FROM `adventureworks2019.Purchasing.PurchaseOrderHeader` po_header
WHERE Status =1 AND EXTRACT(YEAR FROM ModifiedDate) = 2014
GROUP BY 1,2;
```

Here's the table created based on the provided data:

| Row | year | Status | order_cnt | value          |
|-----|------|--------|-----------|----------------|
| 1   | 2014 | 1      | 224       | 3873579.0123 |

