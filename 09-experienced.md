# Experienced (5+ Years) Questions

### 1. Explain Drupal's architecture.

Modern Drupal is built on Symfony components.  

Main parts:  
- **Kernel** – boots the application  
- **Service Container** – manages services  
- **Routing** – maps URLs to controllers  
- **Entity system** – handles data  
- **Plugin system** – discoverable components  
- **Render system** – turns data into HTML  
- **Twig** – templating  
- **Configuration system** – YAML-based config  

It is modular, event-driven, and follows modern PHP practices (dependency injection, OOP).

### 2. How do you design scalable Drupal applications?

- Use proper caching strategy (Redis + Varnish + CDN)  
- Design clean content architecture  
- Avoid heavy Views when possible  
- Use queue workers for background tasks  
- Keep custom code lean and well-tested  
- Use configuration splits for different environments  
- Plan for horizontal scaling (multiple web servers)  
- Monitor performance continuously  
- Prefer headless architecture for very high traffic if needed  

### 3. What are the best practices for module development?

- Follow Drupal coding standards  
- Use dependency injection  
- Prefer plugins and events over hooks when possible  
- Write automated tests  
- Keep modules focused (one responsibility)  
- Document your code  
- Use configuration schema  
- Make modules uninstallable cleanly  
- Avoid hard-coded values  

### 4. How do you handle configuration across environments?

- Use Configuration Management (export/import)  
- Use Config Split module for environment-specific config  
- Store config in Git  
- Use `drush cex` and `drush cim`  
- Never edit config directly in production  
- Use environment variables or settings.php for secrets  

### 5. Explain deployment workflows using Composer, Drush, and Git.

Typical flow:  
1. Develop on local (Git branch)  
2. Commit code + config  
3. Push to repository  
4. On staging/production:  
   - `git pull`  
   - `composer install --no-dev`  
   - `drush updb`  
   - `drush cim`  
   - `drush cr`  

Many teams use CI/CD (GitHub Actions, GitLab CI, etc.) to automate this.

### 6. How do you write automated tests in Drupal?

Drupal supports:  
- **Unit tests** (pure PHP logic)  
- **Kernel tests** (with Drupal bootstrap but no full browser)  
- **Functional tests** (with browser simulation)  
- **FunctionalJavascript tests**  

You place tests in `tests/src/` and run them with PHPUnit or `drush test`.

### 7. What testing frameworks are supported?

- PHPUnit (main framework)  
- Drupal’s own testing traits and base classes  
- Behat (for behavior-driven tests – contributed)  
- Nightwatch or Playwright for JS (in some setups)

### 8. How do you implement CI/CD for Drupal projects?

Common tools: GitHub Actions, GitLab CI, CircleCI, Bitbucket Pipelines.  

Typical pipeline:  
1. Install Composer dependencies  
2. Run coding standards (phpcs)  
3. Run tests  
4. Build artifacts  
5. Deploy to server (or platform like Acquia, Pantheon, Platform.sh)  

### 9. How do you troubleshoot memory leaks?

- Use tools like Blackfire, Xdebug, or Tideways  
- Check for objects that are never released  
- Look at entity loading in loops (load too many entities)  
- Watch static caches that grow forever  
- Increase memory limit temporarily to confirm  
- Profile the page and find what consumes memory  

### 10. Describe a challenging Drupal project you worked on.

(Prepare your own real story.)  

Example structure:  
- What was the project goal?  
- What were the technical challenges?  
- How did you solve them?  
- What was the result?  

Interviewers love real experience stories.
