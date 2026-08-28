# Database & Performance Questions

### 1. What database systems does Drupal support?

Drupal supports:  
- MySQL / MariaDB (most common)  
- PostgreSQL  
- SQLite (good for small or development sites)  

Drupal 11 needs newer versions (MySQL 8.0+, MariaDB 10.6+, PostgreSQL 16+, etc.).

### 2. What are database abstraction layers?

The database abstraction layer lets Drupal talk to different databases using the same code.  

You write queries using Drupal’s Database API (`\Drupal::database()`), and Drupal converts them to the correct SQL for MySQL, PostgreSQL, or SQLite.  

This makes your code database-independent.

### 3. How do you optimize Drupal performance?

Simple ways:  
- Enable caching (Page cache, Dynamic page cache, Render cache)  
- Use Redis or Memcached for cache backend  
- Use a CDN  
- Optimize images  
- Use BigPipe  
- Enable CSS/JS aggregation  
- Use Views carefully (avoid heavy queries)  
- Keep modules updated and remove unused ones  
- Use Twig debugging only in development  
- Optimize database (indexes, slow query log)

### 4. What is BigPipe?

BigPipe is a performance feature that sends the page in pieces.  

Important parts (like header and main content) load first.  
Slower parts (like personalized blocks) load later.  

This makes the page feel much faster to the user.

### 5. What is lazy loading in Drupal?

Lazy loading means loading images or content only when the user scrolls near them.  

Drupal supports lazy loading for images by default in modern versions.  
This reduces initial page load time and saves bandwidth.

### 6. How do you debug slow queries?

Ways to find slow queries:  
- Enable Drupal’s database logging or use Devel module  
- Use MySQL slow query log  
- Use tools like New Relic, Blackfire, or Tideways  
- Check Views query with “Show the SQL query” option  
- Use `EXPLAIN` on the SQL query  

Then optimize the query or add indexes.

### 7. What caching layers are available in Drupal?

Main caching layers:  
1. **Browser cache**  
2. **CDN / Reverse proxy** (Varnish, Cloudflare)  
3. **Internal Page Cache** (anonymous users)  
4. **Dynamic Page Cache** (logged-in users)  
5. **Render cache**  
6. **Entity cache**  
7. **Twig template cache**  
8. **Database cache tables** or external cache (Redis/Memcached)
