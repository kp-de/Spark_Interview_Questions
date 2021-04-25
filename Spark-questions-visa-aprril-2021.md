First one - how do you build a sampling system for dynamic number of fields in your data?
My Answer: read the data into a Spark type. Iterate over this type to build a list of all fields in the data (as fields are dynamic, we do not know this beforehand). 
Now, iterate over this list to build a Select_Expr expression to implement a case-statement like logic in SQL. Each field in the data gets pivoted to a field in the result
set using case statements. At the end, execute the Select_Expr on the source data frame in a single execution.

Advantage: We are only reading the data once, irrespective of the number of fields in the data.

Second one: How would you implement a system to find if a Product type is present in a particular range or not.

![image](https://user-images.githubusercontent.com/53032061/115989759-8acd5500-a5dd-11eb-9c24-18f26c0bdb46.png)

My Answer: Use ORC bloom filters to find the presence of the Product in each partition. Think about the false negatives of the Hive-ORC bloom filters.

Q: How to implement Kafka's exactly once semantics at the consumer end? (Check other semantics as well, at-most once, at-least once etc.)
