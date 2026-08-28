# Intermediate Drupal Interview Questions

### 1. What are entities in Drupal?

Entities are the basic building blocks of data in Drupal.  
Examples of entities:  
- Nodes (content)  
- Users  
- Taxonomy terms  
- Comments  
- Files  
- Custom entities you create  

Every entity has a unique ID and can have fields attached to it.

### 2. What are fields and field types?

**Fields** are the pieces of information you attach to entities.  
Example: Title, Body, Image, Price, Email.

**Field types** tell Drupal what kind of data the field stores:  
- Text  
- Number  
- Image  
- Date  
- Entity Reference (link to another entity)  
- Boolean (Yes/No)

### 3. What is the Entity API?

The Entity API is the system that lets developers work with entities in code.  
It provides standard ways to:  
- Create entities  
- Load entities  
- Save entities  
- Delete entities  
- Query entities  

It makes working with different entity types consistent.

### 4. Explain hooks in Drupal.

Hooks are special functions that allow modules to change or react to Drupal’s behavior.  
When Drupal does something (like saving a node), it looks for functions named in a special way (example: `mymodule_node_insert()`).  

Hooks are the old (but still used) way to extend Drupal.  
Modern Drupal prefers plugins and events, but hooks are still important.

### 5. What are plugins in Drupal?

Plugins are small pieces of reusable code that do one specific job.  
Examples:  
- Block plugins  
- Field widgets  
- Field formatters  
- Views plugins  

Drupal discovers plugins automatically.  
You create a plugin by writing a class with a special annotation or attribute.

### 6. What is dependency injection in Drupal?

Dependency injection means giving an object the things it needs (services) from outside, instead of creating them inside the class.  

In Drupal, the service container injects the required services into your class automatically.  
This makes code cleaner, easier to test, and more flexible.

### 7. What are services in Drupal?

Services are reusable objects that do specific tasks.  
Examples:  
- Database service  
- Current user service  
- Entity type manager  
- Logger  

You define services in a `*.services.yml` file and inject them where needed.

### 8. What is the Configuration Management system?

Configuration Management (CMI) lets you store site settings (views, content types, fields, etc.) as YAML files.  

You can export configuration from one environment (local) and import it into another (staging or production).  
This keeps all environments in sync.

### 9. What is the difference between configuration and content?

| Configuration | Content |
|---------------|---------|
| Site settings and structure | Actual data users create |
| Stored in YAML files | Stored in database |
| Examples: Content types, Views, Menus, Roles | Examples: Blog posts, Users, Images |
| Can be exported/imported easily | Usually migrated with Migrate module |

### 10. What is Composer, and why is it used with Drupal?

Composer is a tool that manages PHP libraries and dependencies.  

In Drupal:  
- It installs Drupal core and modules  
- It manages versions  
- It downloads required libraries automatically  

Almost every modern Drupal project uses Composer.  
Command example: `composer require drupal/pathauto`

### 11. What is Drush?

Drush is a command-line tool for Drupal.  
It helps you do common tasks quickly from the terminal.  

Examples:  
- `drush cr` → clear cache  
- `drush updb` → run database updates  
- `drush cex` → export configuration  
- `drush en mymodule` → enable a module  

### 12. How do you clear cache in Drupal?

Ways to clear cache:  
1. Admin UI → Configuration → Development → Performance → Clear all caches  
2. Drush: `drush cr` or `drush cache:rebuild`  
3. In code: `\Drupal::service('cache_tags.invalidator')->invalidateTags([...]);`

Clearing cache is very common during development.

### 13. What are Views in Drupal?

Views is a powerful module (now in core) that lets you create custom lists of content without writing code.  

You can:  
- Show latest articles  
- Create tables, grids, lists  
- Filter and sort content  
- Create pages or blocks  

Views is one of the most used features in Drupal.

### 14. What are Display Modes and View Modes?

**View modes** (also called display modes) control how an entity is shown in different places.  

Examples:  
- Full content  
- Teaser  
- RSS  
- Search result  

You can choose different fields and formatters for each view mode.

### 15. What is Twig, and why is it used?

Twig is the templating engine used in Drupal (from Drupal 8 onwards).  

It is used to create the HTML output of the website.  
Twig is safer than plain PHP because it automatically escapes output and has a cleaner syntax.  

Theme developers write Twig templates (`.html.twig` files) to control the design.
