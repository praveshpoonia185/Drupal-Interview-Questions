# Frequently Asked Practical Questions

### 1. What is the difference between hooks, plugins, and services?

| Concept | Purpose | Example |
|---------|---------|---------|
| **Hooks** | React to Drupal events (old style) | `hook_node_insert()` |
| **Plugins** | Small reusable components discovered by Drupal | Block plugin, Field formatter |
| **Services** | Reusable objects managed by the container | Logger, Entity Type Manager |

### 2. When would you use an Event Subscriber instead of a hook?

Use an Event Subscriber when:  
- You want cleaner, object-oriented code  
- You need to subscribe to Symfony or Drupal events  
- You want easier unit testing  
- The logic is complex  

Hooks are still fine for simple changes.

### 3. Explain the request lifecycle in Drupal.

1. Web server receives the request  
2. Drupal kernel boots  
3. Routing matches the URL to a controller or form  
4. Access checks run  
5. Controller or form builds a render array  
6. Render system turns it into HTML  
7. Response is sent to the browser  

Events are fired at many points during this process.

### 4. What is render caching?

Render caching stores the HTML (or render array) of parts of the page so Drupal does not rebuild them every time.  

It uses cache tags, contexts, and max-age to know when to invalidate the cache.

### 5. What is the difference between Block plugins and custom blocks?

| Block Plugin | Custom Block (Content Block) |
|--------------|------------------------------|
| Defined in code | Created in the UI |
| Reusable and version-controlled | Stored in database (content) |
| Good for developers | Good for content editors |
| Example: “Recent content” block in code | A block with body text created by editor |

### 6. How do you create multilingual websites?

Enable the four language modules, add languages, make content and configuration translatable, and use the language switcher.  
See the Scenario-Based section for more details.

### 7. How do you implement custom authentication?

Options:  
- Use Simple OAuth / OAuth2 for APIs  
- Create a custom authentication provider plugin  
- Use external identity providers (SAML, OpenID Connect) with contributed modules  

### 8. How do you optimize Views performance?

- Avoid using too many relationships  
- Use aggregation carefully  
- Enable Views caching  
- Limit the number of results  
- Use indexed fields for filters  
- Prefer entity reference fields over heavy joins  
- Sometimes rewrite the query or use a custom block instead of a heavy View

### 9. Explain cache invalidation using Cache Tags.

When content changes, Drupal invalidates all cache items that have the related cache tags.  

Example: When you update node 15, Drupal clears everything tagged with `node:15`.  
This keeps the cache accurate without clearing the entire cache.

### 10. How do you debug a production issue?

1. Check recent log messages (watchdog)  
2. Look at server error logs  
3. Reproduce on a staging environment if possible  
4. Use monitoring tools (New Relic, etc.)  
5. Temporarily enable more logging  
6. Never enable Twig debug or high error reporting on live production for long  
7. Roll back recent deployments if needed
