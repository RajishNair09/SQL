# SQL
An SQL problem solving

## The process of structured problem solving in SQL can be summarized as follows:

1. **Visualize the required output**: Clearly understand the desired outcome of your query. Determine the columns that need to be included in the result set.

2. **Identify the rows to be selected**: Use filters such as the WHERE and HAVING clauses to specify the conditions that the rows must meet in order to be included in the result set.

3. **Define the data granularity**: If necessary, use aggregations such as the GROUP BY clause to determine the level of detail or granularity at which the data should be grouped.

4. **Consider using CTEs or subqueries**: Complex queries can benefit from the use of Common Table Expressions (CTEs) or subqueries to break down the problem into more manageable parts and improve query organization.

5. **Validate individual sections:** Test and validate each section of the query independently to ensure that it produces the expected results. This helps in identifying any issues or errors early on.

6. **Combine and stitch smaller pieces**: Once you have validated the individual sections, combine them together to obtain the entire solution. This may involve using joins to combine data from multiple tables.

7. **Check for row explosion**: When performing joins, be cautious of potential row explosion, where the number of rows in the result set increases significantly. This can happen if the join conditions are not properly defined or if the data relationships are not accurately represented.

By following these steps, you can effectively structure your problem-solving approach in SQL and write queries that address specific challenges or requirements.

### Below are problems we need to solve :
--------------------------------------------------------------
#### Problem 1

“Get the number of orders by the Type of Transaction excluding the orders shipped from Sangli and Srinagar. Also, exclude the SUSPECTED_FRAUD cases based on the Order Status, and sort the result in the descending order based on the number of orders.”

 
Before we start working on the solution, as pointed out rightly by Shreyas in the video above, we must analyse what the required input parameters are and what the expected output is. This will help to optimise the query. In the problem statement above, the input and output are as follows:

Input: Orders table (Order_Id, Type, Order_City, Order_Status)
Expected output: Type of Transaction | Orders (Sorted in the descending order of Orders)


## Step 1: 

For the first step, ‘Filter out ‘Sangli’ and ‘Srinagar’ from the city column of the data, the solution was to apply the <> filter condition, but the hack was to apply an ‘and’ operator, as shown in the code below.

     

SELECT * FROM orders

WHERE Order_City <>'Sangli' AND Order_City <>'Srinagar'
 

After executing the code given above, in order to check if the result was correct, Shreyas verified the result by displaying all the unique cities by executing the following code:

SELECT Order_City 

FROM (

SELECT * FROM orders

WHERE Order_City <>'Sangli' AND Order_City <>'Srinagar'

) as a

GROUP BY Order_City 
 


## Step 2:

 

Next, we solved the second subpart, ‘Filter out orders that are ‘SUSPECTED_FRAUD’’, using the ‘<>’ filter condition, as shown below. We applied the GROUP BY statement to check all the unique values present in the Order_Status column.

 

SELECT Order_Status

FROM (

SELECT * FROM orders

WHERE Order_City <>'Sangli' AND Order_City <>'Srinagar'

AND Order_Status<>'SUSPECTED_FRAUD'

) as a

GROUP BY Order_Status
 

## Step 3:

 
On executing the code given above, the result displayed did not contain the order status ‘SUSPECTED_FRAUD’. Next, we solved the third subpart, in which we had to count the number of orders for a particular transaction type. We solved this subpart by applying the GROUP BY statement for the column Type, named as Type_of_Transaction, and by applying the count aggregate function to orders_id. We executed the following code for the third step:


SELECT 

Type AS Type_of_Transaction,

COUNT(order_id) as Orders

FROM orders

WHERE Order_City <>'Sangli' AND Order_City <>'Srinagar'

AND Order_Status<>'SUSPECTED_FRAUD'

GROUP BY Type_of_Transaction
 

## Step 4:

 
The final subpart was the simplest of all, in which we had to sort the orders for a particular type of transaction in descending order. We solved this subpart by applying the ORDER BY function, followed by the keyword DESC, thereby completing the problem statement. We got the following code as the final solution:

 

SELECT 

Type AS Type_of_Transaction,

COUNT(order_id) as Orders

FROM orders

WHERE Order_City <>'Sangli' AND Order_City <>'Srinagar'

AND Order_Status<>'SUSPECTED_FRAUD'

GROUP BY Type_of_Transaction

ORDER BY Orders DESC;


![image](https://github.com/RajishNair09/SQL/assets/115383187/ceb5741f-e6c2-48fa-905a-81f636038845)


--------------------------------------------------------------

