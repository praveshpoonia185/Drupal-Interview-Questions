# Security Questions

### 1. How does Drupal prevent SQL injection?

Drupal uses prepared statements and placeholders in its Database API.  

You never write raw user input into SQL.  
Example:  
```php
$query->condition('title', $user_input);
```  
Drupal escapes the value safely. This stops SQL injection attacks.

### 2. What are user roles and permissions?

**Roles** are groups of users (example: Administrator, Editor, Authenticated user, Anonymous).  

**Permissions** are specific actions a role can do (example: create content, edit own content, administer users).  

You assign permissions to roles, and users get the roles.  
This controls what each person can see and do on the site.

### 3. How do you secure a Drupal website?

Simple best practices:  
- Keep Drupal core, modules, and themes updated  
- Use strong passwords and enable 2FA if possible  
- Give users only the permissions they need  
- Use HTTPS  
- Set trusted host patterns  
- Protect the `/admin` and `/user` paths  
- Use security modules if needed (Security Kit, etc.)  
- Regularly check security advisories  
- Do not give write permissions to files directory unnecessarily  
- Use Composer and audit dependencies

### 4. What are trusted host settings?

Trusted host settings prevent HTTP Host header attacks.  

In `settings.php` you set which domain names are allowed:  
```php
$settings['trusted_host_patterns'] = [
  '^www\.example\.com$',
  '^example\.com$',
];
```  
Only requests with these hosts are accepted.

### 5. How do you keep Drupal updated?

1. Check for updates on the Status report page or use `drush pm:security`  
2. Use Composer: `composer update drupal/core --with-dependencies`  
3. Run database updates: `drush updb`  
4. Clear cache  
5. Test on a staging site first  
6. Follow security advisories from drupal.org

### 6. What are security advisories?

Security advisories are official warnings published by the Drupal Security Team when a security problem is found in core or a contributed module.  

They tell you:  
- Which versions are affected  
- How serious the problem is  
- How to fix it (usually by updating)  

Always subscribe or check them regularly.
