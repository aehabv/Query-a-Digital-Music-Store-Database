# Querying a digital music store

![SQL](https://img.shields.io/badge/SQL-003B57?style=flat&logo=sqlite&logoColor=white)
![Chinook](https://img.shields.io/badge/Database-Chinook-2C3E50?style=flat)

Who earns the most, who writes the rock, which employee sells the most, and who's the biggest spender in each country? I answered four questions about a fictional online music store with SQL, then turned the answers into a short slide deck.

The data is the [Chinook](https://github.com/lerocha/chinook-database) sample database: artists, albums, tracks, genres, customers, employees and invoices for an iTunes-style store.

## The questions and what I found

| Question | Answer |
|---|---|
| Which artist has earned the most? | **Iron Maiden** |
| Who's written the most rock songs? | **Led Zeppelin** with 114 tracks, just ahead of **U2** with 112 |
| Which support rep made the most sales? | **Jane Peacock** with $833, nearly 36% of all sales. Margaret Park ($775) and Steve Johnson ($720) follow |
| Who spent the most in each country? | One top customer per country, shown in a chart in the deck |

The queries are in [`QUERIES.txt`](QUERIES.txt), and the charts are in [`PRESENTATION.pdf`](PRESENTATION.pdf) (also as `.pptx`).

## How the queries work

1. **Rock artists:** join artists to albums to tracks to genres, keep rock, and count tracks per artist.
2. **Top earners:** join artists down to invoice lines and add up quantity × unit price.
3. **Sales by employee:** join each support rep to their customers' invoices and total them.
4. **Top customer per country:** a CTE totals spending per customer, a second pass finds each country's maximum, and a join keeps the customers who hit it. If two customers tie, both are kept.

## Caveats

- **Query 4 relies on SQLite being lenient.** Its second pass groups by country but also selects the customer's name and ID, which SQLite allows and stricter databases like PostgreSQL and modern MySQL reject.
- **Earnings means sales.** The store's revenue from an artist's tracks, not what the artist was paid.

## How to run

1. Download `Chinook_Sqlite.sqlite` from the [Chinook repository](https://github.com/lerocha/chinook-database).
2. Open it in [DB Browser for SQLite](https://sqlitebrowser.org/), or run `sqlite3 Chinook_Sqlite.sqlite`.
3. Paste in a query from `QUERIES.txt`.

## What I'd like to do next

Look at trends over time, such as which genres grew or shrank year by year.
