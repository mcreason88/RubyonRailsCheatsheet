## Queries

|                | Active Record                          |SQL                         |          |
|----------------|-------------------------------|-----------------------------|------|
|Find: |`clients = Client.find([1, 10])` |`SELECT * FROM clients WHERE (clients.id IN (1,10)) `  ||
|Find By: |`Client.find_by! first_name: 'Jane'` |`SELECT * FROM clients WHERE (clients.first_name = 'Jane' LIMIT 1`)   |find_by! will raise ActiveRecord::RecordNotFound if no record is found. |
|Passing Params |`Client.where("orders_count = ? AND locked = ?", params[:orders], params[:locked])`|||
|Passing Params as Hash|Client.where("created_at >= :start_date AND created_at <= :end_date", {start_date: params[:start_date], end_date: params[:end_date]})}|||
|Between|`Client.where(created_at: (Time.now.midnight - 1.day)..Time.now.midnight)`|`SELECT FROM clients WHERE(clients.created_at BETWEEN '2020-12-21 00:00:00' AND '2020-12-22 00:00:00')`||
|Subsets: Find using SQL  **IN**|`Client.where(orders_count: [1,3,5])`|`SELECT * FROM clients WHERE (clients.orders_count IN (1,3,5))`||
|Not:|`Client.where.not(locked: true)`|`SELECT * FROM clients WHERE (clients.locked != 1)`||
|Distinct:|`Client.select(:name).distinct`|`SELECT DISTINCT name FROM clients`||
|Limit|`Client.limit(5)`|`SELECT * FROM clients LIMIT 5`||
|Take:|`client = Client.take(2)`|`SELECT * FROM clients LIMIT 2`|Returns record without any implicit ordering.  Returns nil if no record is found.||
|Offset:|`Client.limit(5).offset(30)`|`SELECT * FROM clients LIMIT 5 OFFSET 30`||
|Find or Create a New Object|`Client.find_or_create_by!(first_name: 'Andy')`|`SELECT * FROM clients WHERE(clients.first_name = 'Andy') LIMIT 1 BEGIN INSERT INTO clients(created_at, first_name, updated_at) VALUES ('2011-08-30 05:22:57', 'Andy', '2011-08-30 05:22:57') COMMIT`||
|Find or Initialize a New Object|`jane = Client.find_or_initialize_by(first_name: 'Jane')`|||
|Find by SQL|`Client.find_by_sql("SELECT * FROM clients INNER JOIN orders ON clients.id = orders.client_id ORDER BY clients.created_at desc")`|||
|Exists?|`Client.exists?(1)`|`Client.where(first_name: 'Ryan').exists?`||
||`Client.exists?(name: ['John', 'Sergei']`|||
||`Client.where(first_name: 'Ryan').exists?`|||
|Count|`Client.count`|`SELECT count(*) AS count_all FROM clients`||
|Average|`Client.average("orders_count")`|||
|Minimum and Maximum|`Client.minimum("age")`||minimum/maximum value of a field|
|Sum|`Client.sum("orders_count")`||sum of a field|
|Ordering Results|`Client.order(:orders_count, created_at: :desc)`|||
||`Client.order("orders_count ASC, created_at DESC")`|||
|Chaining ORDER BY|`Client.order("orders_count ASC").order("created_at DESC")`|`SELECT * FROM clients ORDER BY orders_count ASC, created_at DESC`||
![image](https://user-images.githubusercontent.com/102683222/231505271-23a63529-d126-4b4a-ac14-38f4d8c9480f.png)


