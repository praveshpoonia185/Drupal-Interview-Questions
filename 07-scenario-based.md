# Scenario-Based Questions

### 1. How would you migrate a Drupal 7 site to Drupal 10/11?

Simple plan:  
1. Audit the D7 site (modules, custom code, content)  
2. Set up a new Drupal 10/11 site with Composer  
3. Use the Migrate API and Migrate Drupal modules  
4. Migrate users, content, taxonomy, files  
5. Rebuild themes and custom modules for the new version  
6. Test everything carefully  
7. Switch DNS when ready  

Many old modules need to be replaced or rewritten.

### 2. How would you troubleshoot a white screen of death?

Steps:  
1. Check the recent log messages (if you can access admin)  
2. Enable error display in `settings.php` temporarily  
3. Check PHP error logs and web server logs  
4. Clear cache  
5. Disable recently added modules one by one  
6. Check memory limit and PHP version  
7. Use `drush ws` to see watchdog messages  

Usually it is a PHP fatal error or missing dependency.

### 3. How would you improve a slow Drupal website?

1. Enable all caching layers  
2. Use Redis or Memcached  
3. Add a CDN and Varnish if needed  
4. Optimize images and enable lazy loading  
5. Review heavy Views and custom queries  
6. Enable BigPipe  
7. Aggregate and minify CSS/JS  
8. Remove unused modules  
9. Use a performance monitoring tool  

### 4. How would you implement multilingual support?

1. Enable Language, Content Translation, Configuration Translation, Interface Translation modules  
2. Add the languages you need  
3. Configure detection and selection (URL, domain, browser)  
4. Make content types translatable  
5. Translate content and configuration  
6. Use language switcher block  

Drupal has excellent multilingual features out of the box.

### 5. How would you create a custom REST endpoint?

1. Create a custom module  
2. Define a route that points to a controller or a resource plugin  
3. Or create a REST resource plugin  
4. Return JSON data  
5. Add proper permissions and authentication  

For modern projects, many people prefer JSON:API + custom fields or GraphQL.

### 6. How would you debug a custom module?

1. Use `dump()` or `kint()` (with Devel) in code  
2. Check recent log messages  
3. Use Xdebug with an IDE  
4. Enable Twig debugging if theming  
5. Clear cache after changes  
6. Check the Status report for errors  
7. Use `drush php` or `drush eval` for quick tests  

### 7. What steps would you take if Composer dependencies conflict?

1. Read the error message carefully  
2. Check which packages conflict  
3. Try `composer why` or `composer why-not`  
4. Update packages carefully (`composer update package/name`)  
5. Use `composer require` with version constraints  
6. Sometimes remove and re-add the conflicting package  
7. Check Drupal compatibility of the modules  

Always work on a branch and test after resolving conflicts.
