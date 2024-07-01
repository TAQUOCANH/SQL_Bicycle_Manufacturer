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
    
### Calculate Quantity of items, Sales value & Order quantity by each Subcategory in L12M
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
Dưới đây là bảng dữ liệu bạn cung cấp:

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



