| ROUTE | ACTION | METHOD  | DATA FROM CLIENT | DATA FROM SERVER |
| --- 	| --- 		| --- | --- | --- |
| /admin/register 					| send email to create new admin | post | email |  {success message, token} or error |
| /admin/login 						| send token to verify new admin |   get     | token |  {success message, token} or error |
| /products 						| find all products | get | | {success message, products} or error    |
| /products/product_id/:product_id 	| find one product by _id |   get | product_id | {success message, product } or error    |
| /products/add | add a product 	|   post    | name, description, price,  | {success message} or error |admin |
| /products/update 					| update a product |   post    | name, description, price,  | {success message} or error |admin |
| /products/delete/:product_id 		| delete a product |   delete  | product_id | {success message} or error |admin |
| /email/confirmation 				| send an email to the admin (repo on gitlab)  | post | email, title, body | {success message} or error |
| /cart 						| get items from cart | post | cart (_id,qty) | {success message, products} or error |
| /payment 						| pay with stripe (repo on gitlab) |   post | amount, stripe token_id | {success message} or error |
| /update_stock 				| update stock in the DB after payment | post | cart (_id,qty) | {success message} or error |admin |

