# Advanced Drupal Interview Questions

### 1. Explain Drupal's render pipeline.

The render pipeline is how Drupal turns data into HTML.

Simple steps:  
1. Drupal builds a render array (a PHP array that describes what to show).  
2. The render system processes this array.  
3. It applies templates (Twig).  
4. It adds CSS and JS.  
5. It caches the result if possible.  
6. Finally, it sends HTML to the browser.

Render arrays are the heart of how Drupal builds pages.

### 2. What is cache metadata (Cache Tags, Cache Contexts, Max-Age)?

Cache metadata tells Drupal when and how long something can be cached.

- **Cache Tags**: Labels that say “this content depends on these things”.  
  Example: `node:5`, `user:3`. When node 5 changes, all caches with that tag are cleared.

- **Cache Contexts**: Things that change the output for different users or situations.  
  Example: `user.roles`, `url`, `languages`.

- **Max-Age**: How long (in seconds) the cache can stay valid.  
  Example: 3600 = 1 hour. 0 means do not cache.

### 3. How does Drupal caching work?

Drupal has multiple caching layers:

1. **Internal Page Cache** – for anonymous users (full page)  
2. **Dynamic Page Cache** – for authenticated users (parts of the page)  
3. **Render Cache** – caches individual render arrays  
4. **Entity Cache** – caches loaded entities  
5. **BigPipe** – sends page parts as they are ready  

You can also use external tools like Varnish, Redis, or Memcached for better performance.

### 4. What are events and event subscribers?

Events are messages that Drupal (or modules) send when something happens.  
Example: when a user logs in, or when a node is saved.

An **Event Subscriber** is a class that listens for a specific event and runs code when that event happens.

This is the modern way (Symfony style) to react to things instead of using only hooks.

### 5. What is the difference between hooks and events?

| Hooks | Events |
|-------|--------|
| Old Drupal way | Modern Symfony way |
| Function with special name | Class that implements EventSubscriberInterface |
| Harder to test | Easier to test and organize |
| Still widely used | Preferred for new code |

Both can be used. Events are better for complex logic.

### 6. Explain custom entities.

Custom entities are entities you create yourself when core entities (node, user, etc.) are not enough.  

You define:  
- Entity type  
- Base fields  
- Storage  
- Forms, views, routes  

Example: A “Product” entity or “Event Registration” entity.

### 7. What are configuration entities and content entities?

| Content Entities | Configuration Entities |
|------------------|------------------------|
| Store actual data | Store site settings |
| Have revisions usually | Usually no revisions |
| Examples: Node, User, Comment | Examples: View, Content Type, Role, Field storage |
| Stored in database tables | Stored as YAML + database |

### 8. What is the Plugin API?

The Plugin API is the system that discovers and manages plugins.  

Drupal scans for classes with special annotations/attributes and makes them available.  
You can create your own plugin types too.

### 9. How do you create a custom module?

Simple steps:  
1. Create folder: `modules/custom/hello_world`  
2. Create `hello_world.info.yml`  
3. Create `hello_world.module` (optional)  
4. Enable the module with Drush or UI  

That’s the basic start. Then you add routes, controllers, services, etc.

### 10. How do you create custom routes and controllers?

1. Create `hello_world.routing.yml`  
2. Define path, controller class, and method  
3. Create a Controller class that extends `ControllerBase`  
4. Return a render array from the method  

Example route:  
```yaml
hello_world.hello:
  path: '/hello'
  defaults:
    _controller: '\Drupal\hello_world\Controller\HelloController::content'
  requirements:
    _permission: 'access content'
```

### 11. Explain dependency injection with an example.

Instead of creating objects inside a class, you ask Drupal to give them to you.

Example:  
```php
class MyService {
  protected $entityTypeManager;

  public function __construct(EntityTypeManagerInterface $entityTypeManager) {
    $this->entityTypeManager = $entityTypeManager;
  }
}
```

Then in `services.yml`:  
```yaml
services:
  my_module.my_service:
    class: Drupal\my_module\MyService
    arguments: ['@entity_type.manager']
```

### 12. What is a Form API?

Form API is the system to create forms in Drupal.  

You create a class that implements `FormInterface` (usually extends `FormBase`).  
You define:  
- Form ID  
- Build form (fields)  
- Validate form  
- Submit form  

Drupal handles security (CSRF tokens) and form processing for you.

### 13. What are AJAX forms in Drupal?

AJAX forms update only part of the page without full reload.  

You add `#ajax` property to a form element.  
When the user interacts, Drupal sends an AJAX request and updates the form or page using commands.

### 14. Explain Batch API.

Batch API is used for long-running tasks that would timeout if done in one request.  

You break the work into small pieces (operations).  
Drupal shows a progress bar and runs each piece one by one.  

Example: Importing 10,000 users or updating many nodes.

### 15. What is Queue API?

Queue API lets you put tasks in a queue and process them later (usually with cron or a worker).  

Useful for:  
- Sending emails  
- Processing heavy tasks  
- Background jobs  

You create a queue worker plugin that processes each item.
