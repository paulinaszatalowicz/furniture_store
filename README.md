# furniture_store
# The owner of Lauren's furniture store has been collecting transaction data for the past year, but she just discovered that they can't actually organize their data because it hadn't been formatted correctly. The task was to convert the data to make it useful again.

# The owner couldn't sort the purchases, the results were odd. It was so because the purchase_price's type was originally set as a string. I have changed that using:

SELECT 
CAST(purchase_price AS float64)
FROM 
customer_data.customer_purchase
ORDER BY 
CAST(purchase_price AS float64) DESC 

# In order to analyze purchases during december sale I have typecasted a data field, which was actually a datetime type, into an actual data type using the formula:

SELECT 
CAST(date AS date) AS date_only,
purchase_price
FROM 
customer_data.customer_purchase
WHERE 
date BETWEEN '2020-12-01' AND '2020-12-31'

# The owner wanted to know if customers prefer certain colors, so the owner can manage store inventory accordingly. But the product_code is the same, regardless of the product color. I needed to find another way to separate products by color to can tell if customers prefer one color over the others. I have written a query using CONCAT function to create a unique key for products in certain colors (and checked if the query works on the example of couches):

SELECT 
CONCAT(product_code, product_color) AS new_product_code
FROM 
customer_data.customer_purchase
WHERE 
product = 'couch'

# Some of the names in the database was missing, so I have decided to use COALESCE function to enable the dataset to be analyzed. If the product name wasn't available, SQL should check for the product code instead and put the information in newly created column "product_info", so the owner can review the whole list of the products they sold:

SELECT 
COALESCE(product, product_code) AS product_info
FROM 
customer_data.customer_purchase
