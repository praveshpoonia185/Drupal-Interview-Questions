# Additional Backend + Frontend Interview Questions

## Extra Backend Questions

### 1. What is the difference between `hook_form_alter` and `hook_form_FORM_ID_alter`?

- `hook_form_alter` runs for every form.  
- `hook_form_FORM_ID_alter` runs only for one specific form.  

Always prefer the more specific one when possible.

### 2. What is the Entity Query API?

It is a simple way to query entities without writing SQL.  

Example:  
```php
$query = \Drupal::entityQuery('node')
  ->condition('type', 'article')
  ->condition('status', 1)
  ->accessCheck(TRUE)
  ->execute();
```

### 3. What is Config Split?

Config Split is a popular module that lets you have different configuration for different environments (development, staging, production).  
Example: Enable Devel module only on local, not on production.

### 4. What is the difference between `t()` and `$this->t()`?

Both translate strings.  
- `t()` is the global function.  
- `$this->t()` is used inside classes that use the StringTranslationTrait (preferred in modern code).

### 5. How do you add a custom field formatter?

Create a plugin class that extends `FormatterBase` and use the `@FieldFormatter` annotation (or attribute).  
Then it appears in the Manage Display settings.

### 6. What is the State API vs Configuration API?

| State API | Configuration API |
|-----------|-------------------|
| Temporary or environment-specific data | Permanent site configuration |
| Not exported to YAML | Exported to YAML |
| Example: last cron run time | Example: site name, views |

### 7. What is update.php / `drush updb`?

It runs database update hooks (`hook_update_N`) after you update modules or core.  
Always run it after updating code.

## Extra Frontend Questions

### 1. How do you attach a library only on certain pages?

In a preprocess function:  
```php
function mytheme_preprocess_page(&$variables) {
  if (\Drupal::routeMatch()->getRouteName() == 'entity.node.canonical') {
    $variables['#attached']['library'][] = 'mytheme/special';
  }
}
```

### 2. What is the difference between `attributes` and `content_attributes` in node templates?

- `attributes` = attributes for the outer wrapper (usually `<article>`)  
- `content_attributes` = attributes for the content div inside  

### 3. How do you print a field with custom wrapper in Twig?

```twig
<div class="my-custom-class">
  {{ content.field_image }}
</div>
```

Or remove the default wrapper with:  
```twig
{{ content.field_image|without('field_image') }}  {# advanced #}
```

Better: use field templates or preprocess.

### 4. What is `attach_library` vs libraries in info.yml?

- `libraries` in `.info.yml` loads the library on every page.  
- `attach_library` loads it only when needed (better for performance).

### 5. How do you create a custom page template for a specific content type?

Use template suggestion: `page--node--article.html.twig`  
Or more specific: `page--node--1.html.twig`

### 6. What is the purpose of `html.html.twig` and `page.html.twig`?

- `html.html.twig` → the full HTML document (`<html>`, `<head>`, `<body>`)  
- `page.html.twig` → the page structure inside the body (regions, layout)

### 7. How do you add a body class based on content type?

In preprocess:  
```php
function mytheme_preprocess_html(&$variables) {
  if ($node = \Drupal::routeMatch()->getParameter('node')) {
    $variables['attributes']['class'][] = 'node-type-' . $node->bundle();
  }
}
```

### 8. What is HTMX support in recent Drupal?

Drupal 11.3+ has native HTMX support.  
HTMX lets you add dynamic behavior with simple HTML attributes and much less custom JavaScript.

## Mixed / Architecture Questions

### 1. When would you choose a custom entity over a content type (node)?

Use a custom entity when:  
- You need different access rules  
- You do not need revisions or path aliases the same way  
- Performance is critical  
- The data model is very different from normal content  

### 2. How do you keep custom code upgrade-safe?

- Follow Drupal APIs  
- Avoid hacking core  
- Use dependency injection  
- Write tests  
- Keep up with deprecations  
- Use `drupal-check` or PHPStan  

### 3. What is the difference between Drupal CMS and Drupal core?

Drupal CMS (from the Starshot initiative) is a pre-configured, easier-to-use package built on Drupal core + recipes.  
Drupal core is the pure framework/CMS you can build anything with.
