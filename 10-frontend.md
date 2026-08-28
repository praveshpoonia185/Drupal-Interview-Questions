# Frontend (FE) Drupal Interview Questions

### 1. What is theming in Drupal?

Theming is controlling how the website looks.  
You create or customize a theme using Twig templates, CSS, and JavaScript.  
A theme decides the HTML structure, colors, fonts, and layout.

### 2. What is a base theme and a sub-theme?

**Base theme** is a starting theme (example: Olivero, Classy, Stable).  

**Sub-theme** inherits everything from the base theme and lets you override only what you need.  
Best practice: Always create a sub-theme instead of changing the base theme directly.

### 3. What is Twig debugging and how do you enable it?

Twig debugging shows which template is being used and available variables.  

Enable it in `services.yml` (or development.services.yml):  
```yaml
parameters:
  twig.config:
    debug: true
    auto_reload: true
    cache: false
```  
Then clear cache. You will see HTML comments with template suggestions.

### 4. How do you override a Twig template?

1. Find the template name from Twig debug comments.  
2. Copy the template into your theme’s folder (same structure).  
3. Rename it according to the suggestion (example: `node--article--full.html.twig`).  
4. Clear cache.  

Drupal will use your version.

### 5. What are preprocess functions?

Preprocess functions let you change or add variables before the template is rendered.  

Example in your theme’s `.theme` file:  
```php
function mytheme_preprocess_node(&$variables) {
  $variables['custom_text'] = 'Hello from preprocess';
}
```  
Then use `{{ custom_text }}` in the Twig template.

### 6. What are libraries in Drupal themes?

Libraries define CSS and JavaScript files that your theme or module needs.  

You declare them in `mytheme.libraries.yml` and attach them with `{{ attach_library('mytheme/global') }}` or in preprocess.

This is the modern and correct way to add CSS/JS.

### 7. What is Single Directory Components (SDC)?

SDC (available and stable in Drupal 10.3+ / 11) lets you keep all files of a component (Twig, CSS, JS, YAML) in one folder.  

It makes frontend development cleaner and more component-based (similar to modern JS frameworks).

### 8. How do you make a theme responsive?

- Use responsive CSS (media queries or modern CSS)  
- Use a responsive base theme or framework (Bootstrap, Tailwind via libraries)  
- Test on different screen sizes  
- Use Drupal’s responsive image styles  
- Make sure menus and tables work well on mobile  

### 9. What is the difference between a theme and a module for frontend?

Themes control presentation (HTML, CSS, JS).  
Modules can also provide templates and libraries, but their main job is functionality.  

Frontend developers mostly work in themes, but sometimes create modules for reusable components.

### 10. How do you add custom JavaScript in Drupal?

1. Create a library in `*.libraries.yml`  
2. Add your JS file  
3. Attach the library in a template or preprocess function  
4. Use Drupal’s JavaScript behaviors for proper Drupal integration:

```js
(function (Drupal) {
  Drupal.behaviors.myBehavior = {
    attach: function (context, settings) {
      // your code
    }
  };
})(Drupal);
```

### 11. What are template suggestions?

Template suggestions are alternative template names Drupal can use.  

Example for a node:  
- `node.html.twig`  
- `node--article.html.twig`  
- `node--article--full.html.twig`  
- `node--123.html.twig`  

More specific templates override general ones.

### 12. How do you work with regions in a theme?

Define regions in the theme’s `.info.yml` file:  
```yaml
regions:
  header: Header
  content: Content
  sidebar: Sidebar
  footer: Footer
```  
Then print them in `page.html.twig`:  
```twig
{{ page.header }}
{{ page.content }}
```

### 13. What is the difference between `{{ content }}` and `{{ content.field_name }}`?

- `{{ content }}` prints all fields of the entity.  
- `{{ content.field_name }}` prints only that specific field.  

Using individual fields gives you more control over the markup.

### 14. How do you create a custom Twig function or filter?

Create a Twig extension service (see Coding Questions section).  
Register it as a Twig extension in `services.yml`.  
Then you can use your custom filter or function in any template.

### 15. What frontend tools do you use with Drupal?

Common tools:  
- DDEV or Lando for local environment  
- Twig debugging  
- Browser DevTools  
- Stylelint / ESLint  
- Webpack or Vite (for advanced asset building)  
- Storybook (sometimes with SDC)  
- Responsive design testing tools
