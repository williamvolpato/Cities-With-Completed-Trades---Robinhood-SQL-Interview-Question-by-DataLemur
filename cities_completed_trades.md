# Cities With Completed Trades

## Problem Statement (English)

This is the same question as problem #2 in the SQL Chapter of **Ace the Data Science Interview**!

Assume you're given the tables containing completed trade orders and user details in a Robinhood trading system.

Write a query to retrieve the top three cities that have the highest number of completed trade orders listed in descending order. Output the city name and the corresponding number of completed trade orders.

### Tables
#### `trades` Table:
| Column Name | Type     |
|-------------|----------|
| order_id    | integer  |
| user_id     | integer  |
| status      | string   |
| date        | datetime |
| price       | decimal  |

#### `users` Table:
| Column Name | Type     |
|-------------|----------|
| user_id     | integer  |
| city        | string   |
| email       | string   |
| signup_date | datetime |

### Example Input
#### `trades` Table:
| order_id | user_id | status    | date                | price |
|----------|---------|-----------|---------------------|-------|
| 100123   | 101     | Cancelled | 09/17/2022 12:00:00 | 9.80  |
| 100124   | 102     | Completed | 09/17/2022 12:00:00 | 10.00 |
| 100125   | 103     | Completed | 09/17/2022 12:00:00 | 4.80  |
| 100126   | 148     | Completed | 08/25/2022 12:00:00 | 12.00 |
| 100127   | 265     | Completed | 09/27/2022 12:00:00 | 12.00 |

#### `users` Table:
| user_id | city          | email                     | signup_date         |
|---------|---------------|---------------------------|---------------------|
| 101     | San Francisco | rook01@gmail.com          | 01/10/2021 12:00:00 |
| 102     | Boston        | sailor456@gmail.com       | 02/10/2021 12:00:00 |
| 103     | Boston        | kanyonfan123@gmail.com    | 03/15/2021 12:00:00 |
| 148     | Denver        | shadowser@hotmail.com     | 01/09/2022 12:00:00 |
| 265     | San Francisco | houstoncowboy1122@hotmail.com | 05/25/2022 12:00:00 |

### Example Output
| city          | total_orders |
|---------------|--------------|
| San Francisco | 3            |
| Boston        | 2            |
| Denver        | 1            |

---

## Resolução do Problema (Português)

Esta é a mesma questão do problema #2 do capítulo SQL do livro **Ace the Data Science Interview**!

Assuma que você recebeu tabelas contendo informações de ordens de troca concluídas e detalhes de usuários em um sistema de negociação da Robinhood.

Escreva uma consulta para recuperar as três principais cidades que têm o maior número de ordens de troca concluídas, listadas em ordem decrescente. Exiba o nome da cidade e o número correspondente de ordens de troca concluídas.

### Tabelas
#### Tabela `trades`:
| Nome da Coluna | Tipo     |
|----------------|----------|
| order_id       | integer  |
| user_id        | integer  |
| status         | string   |
| date           | datetime |
| price          | decimal  |

#### Tabela `users`:
| Nome da Coluna | Tipo     |
|----------------|----------|
| user_id        | integer  |
| city           | string   |
| email          | string   |
| signup_date    | datetime |

### Exemplo de Entrada
#### Tabela `trades`:
| order_id | user_id | status    | date                | price |
|----------|---------|-----------|---------------------|-------|
| 100123   | 101     | Cancelled | 17/09/2022 12:00:00 | 9.80  |
| 100124   | 102     | Completed | 17/09/2022 12:00:00 | 10.00 |
| 100125   | 103     | Completed | 17/09/2022 12:00:00 | 4.80  |
| 100126   | 148     | Completed | 25/08/2022 12:00:00 | 12.00 |
| 100127   | 265     | Completed | 27/09/2022 12:00:00 | 12.00 |

#### Tabela `users`:
| user_id | city          | email                     | signup_date         |
|---------|---------------|---------------------------|---------------------|
| 101     | San Francisco | rook01@gmail.com          | 10/01/2021 12:00:00 |
| 102     | Boston        | sailor456@gmail.com       | 10/02/2021 12:00:00 |
| 103     | Boston        | kanyonfan123@gmail.com    | 15/03/2021 12:00:00 |
| 148     | Denver        | shadowser@hotmail.com     | 09/01/2022 12:00:00 |
| 265     | San Francisco | houstoncowboy1122@hotmail.com | 25/05/2022 12:00:00 |

### Exemplo de Saída
| cidade        | total_ordens |
|---------------|--------------|
| San Francisco | 3            |
| Boston        | 2            |
| Denver        | 1            |

---

## Solution (SQL Query)

### English
The SQL query to solve the problem is as follows:

### Português
A consulta SQL para resolver o problema é a seguinte:

```sql
SELECT 
    users.city,
    COUNT(trades.order_id) AS total_orders
FROM 
    trades
JOIN 
    users
ON 
    trades.user_id = users.user_id
WHERE 
    trades.status = 'Completed'
GROUP BY 
    users.city
ORDER BY 
    total_orders DESC
LIMIT 3;
```



---

## Explanation (Explicação)

1. **Join**: We join the `trades` table with the `users` table using the `user_id` column.
2. **Filter (Where Clause)**: Filter only the rows where the trade status is 'Completed'.
3. **Count**: Count the number of completed orders for each city.
4. **Group By**: Group the results by city.
5. **Order By**: Sort the results in descending order based on the number of completed orders.
6. **Limit**: Select only the top 3 cities with the highest number of completed orders.

---
