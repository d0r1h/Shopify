
## Question 1 [Data Analysis]

For Quesion one check this [notebook](https://github.com/d0r1h/Shopify/blob/main/Question1.ipynb)


## Question 2 [SQL]

Question1: How many orders were shipped by Speedy Express in total?

```sql
select ShipperName, count(*)  as 'Total Orders' from (
select S.ShipperName, S.ShipperID, O.OrderID from orders O 
join shippers S 
on S.ShipperID = O.ShipperID ) as t
where ShipperName = 'Speedy Express'
group by ShipperName;
```

output --> 54

Question2: What is the last name of the employee with the most orders?

```sql
select E.EmployeeID, E.LastName, count(*) as 'Order Count' from employees as E
join orders as O
on E.EmployeeID = O.EmployeeID
group by E.EmployeeID
order by count(*) desc
limit 1;
```

output --> 'Peacock'

Question3: What product was ordered the most by customers in Germany?


```sql
select ProductID, sum(Quantity) as 'Total Orders', Country, ProductName from (
select OD.OrderID, C.CustomerID, OD.ProductID, OD.Quantity, C.Country, P.ProductName
from orders as O
join OrderDetails as OD
on OD.OrderID = O.OrderID 
join products as P
on P.ProductID = OD.ProductID
join customers as C
on C.CustomerID = O.CustomerID
where C.Country = 'Germany'
order by OD.Quantity desc
) as t
group by ProductID
order by sum(Quantity) desc
limit 1;

```

output --> 'Boston Crab Meat'
