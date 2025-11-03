# Solution Code - SQL 06 Top Performing Products

<details>
<summary> Step 2 Solution - Practice a Basic Join</summary>
    
```sql
    SELECT t.tournament_id, t.name, ti.purchase_date
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    LIMIT 5;
```
</details>
<summary> Step 3 Solution - Apply the Join for Reporting</summary>
<details>

```sql
    SELECT t.name, ti.ticket_id
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    LIMIT 10;
```
</details>
<details>
   
<summary> Step 4 Solution - Count Tickets per Tournament</summary>
    
 ```sql
    SELECT 
      t.name,
      ti.ticket_id,
      COUNT(*) AS total_sales
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    GROUP BY t.name;
 ```
</details>
 <details>
   
<summary> Step 5 Solution - Rank the Leaderboard</summary>
  
  ```sql
    SELECT 
      t.name,
      ti.ticket_id,
      COUNT(*) AS total_sales
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    GROUP BY t.name
    ORDER BY total_sales DESC, t.name ASC
    LIMIT 15;
  ```
</details>
<details>
=    
<summary> Step 6 Solution - Make the List Reporting-Ready</summary>
    
  ```sql
    -- Exclude cancelled events
    SELECT 
      t.name,
      ti.ticket_id,
      COUNT(*) AS total_sales
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    WHERE t.status <> 'cancelled'
    GROUP BY t.name
    ORDER BY total_sales DESC, t.name ASC
    LIMIT 15;
    
    -- Show only tournaments that are active and visible
    SELECT 
      t.name,
      ti.ticket_id,
      COUNT(*) AS total_sales
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    WHERE t.is_listed = 1 AND t.is_active = 1
    GROUP BY t.name
    ORDER BY total_sales DESC, t.name ASC
    LIMIT 15;
    
    -- Focus on a small date range
    SELECT 
      t.name,
      ti.ticket_id,
      COUNT(*) AS total_sales
    FROM tickets AS ti
    INNER JOIN tournaments AS t
      ON ti.tournament_id = t.tournament_id
    WHERE ti.purchase_date BETWEEN '2025-10-01' AND '2025-10-14'
    GROUP BY t.name
    ORDER BY total_sales DESC, t.name ASC
    LIMIT 15;
  ```
</details>
