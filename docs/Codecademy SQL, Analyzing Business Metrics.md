---

[TOC]

---

**Foreword**

Code snippets. With SQLite. From Codecademy in collaboration with [Periscope Data](https://www.periscopedata.com).

---

## Specifying Comments

- Line comment. This is indicated by two negative signs (eg. ). The remainder of the text on the line is the comment.
- Block comment. The start of the block comment is indicated by /*, the end of the comment by the same string. A block comment can cover text in part of a line, or can span multiple lines.
- Rem or @. For Oracle, a line starting with either REM or @ is a comment line.

## Avanced Aggregates

At the heart of every great business decision is data. Since most businesses store critical data in SQL databases, a deep understanding of SQL is a necessary skill for every data analyst.

Chief among data analysis tasks is data aggregation, the grouping of data to express in summary form. We'll be working with SpeedySpoon, a meal delivery app. The folks at SpeedySpoon have asked us to look into their deliveries and help them optimize their process.

This course was developed in partnership with our good friends at Periscope Data. If you're new to SQL, we recommend you do this course first.

Complete each query by replacing the comments /**/ with SQL code.

We'll start by looking at SpeedySpoon's data. The orders table has a row for each order of a SpeedySpoon delivery. It says when the order took place, and who ordered it.

Add code to the select statement to select all columns in the orders table.

```sql
select *
from /**/
order by id
limit 100;
```

Note that the order and limit clauses keep the data organized.

```sql
SELECT * FROM orders ORDER BY id LIMIT 100;
```

The order_items table lists the individual foods and their prices in each order. Complete the query to select all columns in the order_items table.

```sql
SELECT * FROM order_items ORDER BY id LIMIT 100;
```

Now that we have a good handle on our data, let's dive into some common business queries. We'll begin with the Daily Count of orders placed. To make our Daily Count metric, we'll focus on the date function and the ordered_at field.

To get the Daily Metrics we need the date. Most dates in databases are timestamps, which have hours and minutes, as well as the year, month, and day. Timestamps look like 2015-01-05 14:43:31, while dates are the first part: 2015-01-05.

We can easily select the date an item was ordered at with the date function and the ordered_at field:

```sql
SELECT date(ordered_at)
FROM orders;
```

Let's get a Daily Count of orders from the orders table. Complete the query using the date function to cast the timestamps in ordered_at to dates.

```sql
​SELECT date(ordered_at)
FROM orders
ORDER BY 1
LIMIT 100;
```

The order by 1 statement is a shortcut for order by date(ordered_at). The 1 refers to the first column.

Now that we can convert timestamps to dates, we can count the Orders Per Date. Generally, when we count all records in a table we run a query with the count function, as follows:

```sql
SELECT count(1)
FROM users;
```

This will treat all rows as a single group, and return one row in the result set - the total count.

To count orders by their dates, we'll use the date and count functions and pair them with the group by clause. Together this will count the records in the table, grouped by date.

For example, to see the user records counted by the date created, we use the date and count functions and group by clause as follows:

```sql
SELECT date(created_at), count(1)
FROM users
GROUP BY date(created_at)
```

Use the date and count functions and group by clause to count and group the orders by the dates they were ordered_at.

```sql
SELECT date(ordered_at), count(1)
FROM orders
GROUP BY 1
ORDER BY 1;
```

Group before ordering

We have the Daily Count of orders, but what we really want to know is revenue. How much money has SpeedySpoon made from orders each day?

We can make a few changes to our Daily Count query to get the revenue.

First, instead of using count(1) to count the rows per date, we'll use round(sum(amount_paid), 2) to add up the revenue per date. Complete the query by adding revenue per date.

Second, we need to join in the order_items table because that table has an amount_paid column representing revenue. Complete the query by adding a join clause where orders.id = order_items.order_id.

Note that the round function rounds decimals to digits, based on the number passed in. Here round(..., 2) rounds the sum paid to two digits.

```sql
SELECT date(ordered_at), round(sum(amount_paid), 2)
FROM orders JOIN order_items ON 
	orders.id = order_items.order_id
GROUP BY 1
ORDER BY 1;
```

Now with a small change, we can find out how much we're making per day for any single dish. What's the daily revenue from customers ordering kale smoothies? Complete the query by using a where clause to filter the daily sums down to orders where the name = 'kale-smoothie'.

```sql
SELECT date(ordered_at), round(sum(amount_paid), 2)
FROM orders JOIN order_items ON 
	orders.id = order_items.order_id
WHERE name = 'kale-smoothie'
GROUP BY 1
ORDER BY 1;
```

It looks like the smoothies might not be performing well, but to be sure we need to see how they're doing in the context of the other order items. We'll look at the data several different ways, the first of which is determining what percent of revenue these smoothies represent.

To get the percent of revenue that each item represents, we need to know the total revenue of each item. We will later divide the per-item total with the overall total revenue.

The following query groups and sum the products by price to get the total revenue for each item. Complete the query by passing in sum(amount_paid) into the round function and rounding to two decimal places.

```sql
SELECT name, round(sum(amount_paid), 2)
FROM order_items
GROUP BY name
ORDER BY 2 DESC;
```

We have the sum of the the products by revenue, but we still need the percent. For that, we'll need to get the total using a subquery. A subquery can perform complicated calculations and create filtered or aggregate tables on the fly.

Subqueries are useful when you want to perform an aggregation outside the context of the current query. This will let us calculate the overall total and per-item total at the same time.

Complete the denominator in the subquery, which is the total revenue from order_items. Use the sum function to query the amount_paid from the order_items table.

We now have the percent or revenue each product represents!

```sql
SELECT name, round(sum(amount_paid) / 
	(SELECT sum(amount_paid) FROM order_items) * 100.0, 2)
FROM order_items
GROUP BY 1
ORDER BY 2 DESC;
```

Here order by 2 desc sorts by the second column (the percent) to show the products in order of their contribution to revenue.

As we suspected, kale smoothies are not bringing in the money. And thanks to this analysis, we found what might be a trend - several of the other low performing products are also smoothies. Let's keep digging to find out what's going on with these smoothies.

To see if our smoothie suspicion has merit, let's look at purchases by category. We can group the order items by what type of food they are, and go from there. Since our order_items table does not include categories already, we'll need to make some!

Previously we've been using group by with a column (like order_items.name) or a function (like date(orders.ordered_at)).

We can also use group by with expressions. In this case a case statement is just what we need to build our own categories. case statements are similar to if/else in other languages. Here's the basic structure of a case statement:

```sql
CASE {condition}
	WHEN {value1} THEN {result1}
	WHEN {value2} THEN {result2}
	ELSE {result3}
END
```

We'll build our own categories using a case statement. Complete the query below with a case condition of name that lists out each product, and decides its group.

```sql
SELECT *,
	CASE name
		WHEN 'kale-smoothie'    THEN 'smoothie'
		WHEN 'banana-smoothie'  THEN 'smoothie'
		WHEN 'orange-juice'     THEN 'drink'
		WHEN 'soda'             THEN 'drink'
		WHEN 'blt'              THEN 'sandwich'
		WHEN 'grilled-cheese'   THEN 'sandwich'
		WHEN 'tikka-masala'     THEN 'dinner'
		WHEN 'chicken-parm'     THEN 'dinner'
		ELSE 'other'
	END AS category
FROM order_items
ORDER BY id
LIMIT 100;
```

Complete the query by using the category column created by the case statement in our previous revenue percent calculation. Add the denominator that will sum the amount_paid.

```sql
SELECT
	CASE name
		WHEN 'kale-smoothie'    THEN 'smoothie'
		WHEN 'banana-smoothie'  THEN 'smoothie'
		WHEN 'orange-juice'     THEN 'drink'
		WHEN 'soda'             THEN 'drink'
		WHEN 'blt'              THEN 'sandwich'
		WHEN 'grilled-cheese'   THEN 'sandwich'
		WHEN 'tikka-masala'     THEN 'dinner'
		WHEN 'chicken-parm'     THEN 'dinner'
		ELSE 'other'
	END AS category, round(1.0 * sum(amount_paid) / (SELECT sum(amount_paid) FROM order_items) * 100, 2) AS pct
FROM order_items
GROUP BY 1
ORDER BY 2 DESC;
```

Here 1.0 * is a shortcut to ensure the database represents the percent as a decimal.

 It's true that the whole smoothie category is performing poorly compared to the others. We'll certainly take this discovery to SpeedySpoon. Before we do, let's go one level deeper and figure out why.

While we do know that kale smoothies (and drinks overall) are not driving a lot of revenue, we don't know why. A big part of data analysis is implementing your own metrics to get information out of the piles of data in your database.

In our case, the reason could be that no one likes kale, but it could be something else entirely. To find out, we'll create a metric called reorder rate and see how that compares to the other products at SpeedySpoon.

We'll define reorder rate as the ratio of the total number of orders to the number of people making those orders. A lower ratio means most of the orders are reorders. A higher ratio means more of the orders are first purchases.

Let's calculate the reorder ratio for all of SpeedySpoon's products and take a look at the results. Counting the total orders per product is straightforward. We count the distinct order_ids (different) in the order_items table.

Complete the query by passing in the distinct keyword and the order_id column name into the count function

Here's a hint on how to use the count function to count distinct columns in a table.

```sql
SELECT DISTINCT column_name FROM table_name;
SELECT column_name FROM table_name GROUP BY column_name;

SELECT name, count(DISTINCT order_id)
FROM order_items
GROUP BY 1
ORDER BY 1;
```

Now we need the number of people making these orders.

To get that information, we need to join in the orders table and count unique values in the delivered_to field, and sort by the reorder_rate.

Complete the query below. The numerator should count the distinct order_ids. The denominator should count the distinct values of the orders table's delivered_to field (orders.delivered_to).

```sql
SELECT name, round(1.0 * 
count(DISTINCT order_id) /
	count(DISTINCT delivered_to), 2) AS reorder_rate
FROM order_items
	JOIN orders ON
		orders.id = order_items.order_id
GROUP BY 1
ORDER BY 2 DESC;
```

That's unexpected. While smoothies aren't making a lot of money for SpeedySpoon, they have a very high reorder rate. That means these smoothie customers are strong repeat customers.

Instead of recommending smoothies be taken off the menu, we should talk to the smoothie customers and see what they like so much about these smoothies. There could be an opportunity here to expand the product line, or get other customers as excited as these kale fanatics. Nice work!

Let's generalize what we've learned so far:

- Data aggregation is the grouping of data in summary form.

- Daily Count is the count of orders in a day.

- Daily Revenue Count is the revenue on orders per day.

- Product Sum is the total revenue of a product.

- Subqueries can be used to perform complicated calculations and create filtered or aggregate tables on the fly.

- Reorder Rate is the ratio of the total number of orders to the number of people making orders.

2.Common Metrics

As a data scientist, when you're not investigating spikes or dips in your data, you might be building dashboards of KPIs, or key performance indicators for a company.

KPIs are often displayed on TVs on the walls of the office, and serve as high level health metrics for the business. While every company's metrics are defined slightly differently, the basics are usually very similar.

In this lesson we'll take a look at basic KPIs like Daily Revenue, Daily Active Users, ARPU, and Retention for a video game, Mineblocks.

This company has two tables, gameplays and purchases. The purchases table lists all purchases made by players while they're playing Mineblocks. Complete the query to select from purchases.

```sql
SELECT * FROM purchases ORDER BY id LIMIT 10;
```

The gameplays table lists the date and platform for each session a user plays. Select from gameplays.

```sql
SELECT * FROM gameplays ORDER BY id LIMIT 10;
```

At the heart of every company is revenue, and Mineblocks is no exception. For our first KPI we'll calculate daily revenue.

Daily Revenue is simply the sum of money made per day.

To get close to Daily Revenue, we calculate the daily sum of the prices in the purchases table. Complete the query by using the sum function and passing the price column from the purchases table. 

```sql
SELECT 
	date(created_at),
	round(sum(price),2)
FROM purchases
GROUP BY 1
ORDER BY 1;
```

Update our daily revenue query to exclude refunds. Complete the query by filtering for refunded_at is not null. Update our daily revenue query to exclude refunds. Complete the query by filtering for refunded_at is not null.

Mineblocks is a game, and one of the core metrics to any game is the number people who play each day. That KPI is called Daily Active Users, or DAU.

DAU is defined as the number of unique players seen in-game each day. It's important not to double count users who played multiple times, so we'll use distinct in our count function.

Likewise, Weekly Active Users (WAU) and Monthly Active Users (MAU) are in the same family.

For Mineblocks, we'll use the gameplays table to calculate DAU. Each time a user plays the game, their session is recorded in gameplays. Thus, a distinct count of users per day from gameplays will give us DAU.

Calculate Daily Active Users for Mineblocks. Complete the query's count function by passing in the distinct keyword and the user_id column name.

```sql
SELECT
	date(created_at), 
	COUNT(DISTINCT user_id) AS dau
FROM gameplays
GROUP BY 1
ORDER BY 1;
```

Since Mineblocks is on multiple platforms, we can calculate DAU per-platform.

Previously we calculated DAU only per day, so the output we wanted was [date, dau_count]. Now we want DAU per platform, making the desired output [date, platform, dau_count].

Calculate DAU for Mineblocks per-platform. Complete the query below. You will need to select the platform column and add a count function by passing in the distinct keyword and the user_id column name.

```sql
SELECT
	date(created_at), 
	platform,
	COUNT(DISTINCT user_id) AS dau
FROM gameplays
GROUP BY 1, 2
ORDER BY 1, 2;
```

 group by 1 (date), 2 (platform)
 order by 1 (date), 2 (platform)

We've looked at DAU and Daily Revenue in Mineblocks. Now we must understand the purchasing habits of our users.

Mineblocks, like every freemium game, has two types of users:

    purchasers: users who have bought things in the game
    players: users who play the game but have not yet purchased

The next KPI we'll look at Daily ARPPU - Average Revenue Per Purchasing User. This metric shows if the average amount of money spent by purchasers is going up over time.

Daily ARPPU is defined as the sum of revenue divided by the number of purchasers per day.

To get Daily ARPPU, modify the daily revenue query from earlier to divide by the number of purchasers.

Complete the query by adding a numerator and a denominator. The numerator will display daily revenue, or sum the price columns. The denominator will display the number of purchasers by passing the distinct keyword and the user_id column name into the count function.

```sql
SELECT
	date(created_at), 
	round(sum(price) / COUNT(DISTINCT user_id), 2) AS arppu
FROM purchases
WHERE refunded_at IS NULL
GROUP BY 1
ORDER BY 1;
```

The more popular (and difficult) cousin to Daily ARPPU is Daily ARPU, Average Revenue Per User. ARPU measures the average amount of money we're getting across all players, whether or not they've purchased.

ARPPU increases if purchasers are spending more money. ARPU increases if more players are choosing to purchase, even if the purchase size stays consistent.

No one metric can tell the whole story. That's why it's so helpful to have many KPIs on the same dashboard.

Daily ARPU is defined as revenue divided by the number of players, per-day. To get that, we'll need to calculate the daily revenue and daily active users separately, and then join them on their dates.

One way to easily create and organize temporary results in a query is with CTEs, Common Table Expressions, also known as with clauses. The with clauses make it easy to define and use results in a more organized way than subqueries. These clauses usually look like this:

```sql
WITH {subquery_name} AS (
	{subquery_body}
)
SELECT ...
FROM {subquery_name}
WHERE ...
```

Use a with clause to define daily_revenue and then select from it.

```sql
daily_revenue AS (
	SELECT
		date(created_at) AS dt,
		round(sum(price), 2) AS rev
	FROM purchases
	WHERE refunded_at IS NULL
	GROUP BY 1
)
SELECT * FROM daily_revenue ORDER BY dt;
```

Use a with clause to define daily_revenue and then select from it.

```sql
WITH daily_revenue AS (
	SELECT
		date(created_at) AS dt,
		round(sum(price), 2) AS rev
	FROM purchases
	WHERE refunded_at IS NULL
	GROUP BY 1
)
SELECT * FROM daily_revenue ORDER BY dt;
```

Now you're familiar with using the with clause to create temporary result sets.

You just built the first part of ARPU, daily_revenue. From here we can build the second half of ARPU in our with clause, daily_players, and use both together to create ARPU.

Building on this CTE, we can add in DAU from earlier. Complete the query by calling the DAU query we created earlier, now aliased as daily_players:

```sql
WITH daily_revenue AS (
	SELECT
		date(created_at) AS dt,
		round(sum(price), 2) AS rev
	FROM purchases
	WHERE refunded_at IS NULL
	GROUP BY 1
),
daily_players AS (
	SELECT
		date(created_at) AS dt,
		COUNT(DISTINCT user_id) AS players
	FROM gameplays
	GROUP BY 1
)
SELECT * FROM daily_players
ORDER BY dt;
```

Now that we have the revenue and DAU, join them on their dates and calculate daily ARPU. Complete the query by adding the keyword using in the join clause.

```sql
WITH daily_revenue AS (
	SELECT
		date(created_at) AS dt,
		round(sum(price), 2) AS rev
	FROM purchases
	WHERE refunded_at IS NULL
	GROUP BY 1
),
daily_players AS (
	SELECT
		date(created_at) AS dt,
		COUNT(DISTINCT user_id) AS players
	FROM gameplays
	GROUP BY 1
)
SELECT 
	daily_revenue.dt,
	daily_revenue.rev /
	daily_players.players
FROM daily_players
JOIN daily_players USING (dt);
```

In the final select statement, daily_revenue.dt represents the date, while daily_revenue.rev / daily_players.players is the daily revenue divided by the number of players that day. In full, it represents how much the company is making per player, per day.

In our ARPU query, we used using instead of on in the join clause. This is a special case join.

```sql
FROM daily_revenue JOIN daily_players USING (dt);
```

When the columns to join have the same name in both tables you can use USING instead of on. Our use of the using keyword is in this case equivalent to this clause:

```sql
FROM daily_revenue JOIN daily_players ON daily_revenue.dt = daily_players.dt;

JOIN daily_players USING (dt);
JOIN daily_players ON daily_revenue.dt = daily_players.dt;
```

Now let's find out what percent of Mineblock players are returning to play the next day. This KPI is called 1 Day Retention.

Retention can be defined many different ways, but we'll stick to the most basic definition. For all players on Day N, we'll consider them retained if they came back to play again on Day N+1.

This will let us track whether or not Mineblocks is getting "stickier" over time. The stickier our game, the more days players will spend in-game.

And more time in-game means more opportunities to monetize and grow our business.

Before we can calculate retention we need to get our data formatted in a way where we can determine if a user returned.

Currently the gameplays table is a list of when the user played, and it's not easy to see if any user came back.

By using a self-join, we can make multiple gameplays available on the same row of results. This will enable us to calculate retention.

The power of self-join comes from joining every row to every other row. This makes it possible to compare values from two different rows in the new result set. In our case, we'll compare rows that are one date apart from each user.

To calculate retention, start from a query that selects the date(created_at) as dt and user_id columns from the gameplays table.

```sql
SELECT
	date(created_at) AS dt,
	user_id
FROM gameplays AS g1
ORDER BY dt
LIMIT 100;
```

Now we'll join gameplays on itself so that we can have access to all gameplays for each player, for each of their gameplays.

This is known as a self-join and will let us connect the players on Day N to the players on Day N+1. In order to join a table to itself, it must be aliased so we can access each copy separately.

We aliased gameplays in the query above because in the next step, we need to join gameplays to itself so we can get a result selecting [date, user_id, user_id_if_retained].

Complete the query by using a join statement to join gameplays to itself on user_id using the aliases g1 and g2.

```sql
SELECT
	date(g1.created_at) as dt,
	g1.user_id
FROM gameplays AS g1
JOIN gameplays AS g2 ON
	g1.user_id = g2.user_id
ORDER BY 1
LIMIT 100;
```

We don't use the using clause here because the join is about to get more complicated.

Now that we have our gameplays table joined to itself, we can start to calculate retention.

1 Day Retention is defined as the number of players who returned the next day divided by the number of original players, per day. Suppose 10 players played Mineblocks on Dec 10th. If 4 of them play on Dec 11th, the 1 day retention for Dec 10th is 40%.

The previous query joined all rows in gameplays against all other rows for each user, making a massive result set that we don't need.

We'll need to modify this query.

```sql
SELECT
  date(g1.created_at) AS dt,
  g1.user_id,
  g2.user_id
FROM gameplays AS g1
  JOIN gameplays AS g2 ON
    g1.user_id = g2.user_id
    AND /**/
ORDER BY 1
LIMIT 100;
```

Complete the query above such that the join clause includes a date join:

```sql
date(g1.created_at) = date(datetime(g2.created_at, '-1 day'))
```

This means "only join rows where the date in g1 is one less than the date in g2", which makes it possible to see if users have returned!

```sql
SELECT
	date(g1.created_at) as dt,
	g1.user_id,
	g2.user_id
FROM gameplays AS g1
JOIN gameplays AS g2 ON
	g1.user_id = g2.user_id
	AND date(g1.created_at) = date(datetime(g2.created_at, '-1 day'))
ORDER BY 1
LIMIT 100;
```

The query above won't return meaningful results because we're using an inner join. This type of join requires that the condition be met for all rows, effectively limiting our selection to only the users that have returned.

Instead, we want to use a left join, this way all rows in g1 are preserved, leaving nulls in the rows from g2 where users did not return to play the next day.

Change the join clause to use left join and count the distinct number of users from g1 and g2 per date.

```sql
SELECT
	date(g1.created_at) as dt,
	count(DISTINCT g1.user_id) as total_users,
	count(DISTINCT g2.user_id) as retained_users
FROM gameplays AS g1
LEFT JOIN gameplays AS g2 ON
	g1.user_id = g2.user_id
	AND date(g1.created_at) = date(datetime(g2.created_at, '-1 day'))
GROUP BY 1
ORDER BY 1
LIMIT 100;
```

Now that we have retained users as count(distinct g2.user_id) and total users as count(distinct g1.user_id), divide retained users by total users to calculate 1 day retention!

```sql
SELECT
	date(g1.created_at) as dt,
	round(100 * count(DISTINCT g2.user_id) / count(DISTINCT g1.user_id)) AS retention
FROM gameplays AS g1
LEFT JOIN gameplays AS g2 ON
	g1.user_id = g2.user_id
	AND date(g1.created_at) = date(datetime(g2.created_at, '-1 day'))
GROUP BY 1
ORDER BY 1
LIMIT 100;
```

While every business has different metrics to track their success, most are based on revenue and usage.

The metrics in this lesson are merely a starting point, and from here you'll be able to create and customize metrics to track whatever is most important to your company.

And remember, data science is exploratory! The current set of metrics can always be improved and there's usually more to any spike or dip than what immediately meets the eye.

Let's generalize what we've learned so far:

- Key Performance Indicators are high level health metrics for a business.
- Daily Revenue is the sum of money made per day.
- Daily Active Users are the number of unique users seen each day.
- Daily Average Revenue Per Purchasing User (ARPPU) is the average amount of money spent by purchasers each day.
- Daily Average Revenue Per User (ARPU) is the average amount of money across all users.
- 1 Day Retention is defined as the number of players from Day N who came back to play again on Day N+1.
