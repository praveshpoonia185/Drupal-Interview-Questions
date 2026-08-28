# Beginner Drupal Interview Questions

### 1. What is Drupal?

Drupal is a free and open-source content management system (CMS).  
It is written in PHP.  
People use it to build websites and web applications easily.  
You can manage content, users, and design without writing too much code.

### 2. What are the key features of Drupal?

- Modular system (you can add features with modules)
- Flexible content types and fields
- Strong user roles and permissions
- Multilingual support (many languages)
- Good security
- Themes for design
- Views to display content in different ways
- API support for headless/decoupled sites
- Works well for small to very large websites

### 3. What is the difference between Drupal 7, Drupal 9, Drupal 10, and Drupal 11?

| Version | Main Points |
|---------|-------------|
| **Drupal 7** | Old version. Uses procedural PHP. End of life (no more security updates). |
| **Drupal 9** | Cleaner code after Drupal 8. Removed old deprecated code. Used Symfony 4. |
| **Drupal 10** | Modern. Uses CKEditor 5, Symfony 6, better admin theme (Olivero). Requires PHP 8.1+. |
| **Drupal 11** | Latest. Uses PHP 8.3+, Symfony 7. Has Recipes, Single Directory Components (SDC), better performance, HTMX support, improved navigation. Removed many old modules from core. |

**Simple tip:** Always work with Drupal 10 or 11 now. Drupal 7 is outdated.

### 4. What are nodes in Drupal?

A node is a piece of content on the website.  
Examples: a blog post, a page, an article, a product.  
Every content item is a node.  
Each node has a unique ID (nid).

### 5. What is a content type?

A content type is a template for content.  
Example:  
- Article (has title, body, image, tags)  
- Basic page (has only title and body)  
- Product (has price, description, image)  

You can create your own content types and add different fields to them.

### 6. What are taxonomy and vocabularies?

**Taxonomy** is the system to organize and categorize content.  

**Vocabulary** is a group of terms (categories).  
Example:  
- Vocabulary = "Topics"  
- Terms = Technology, Sports, News  

You can tag content with these terms so users can filter and find content easily.

### 7. What are blocks and regions?

**Blocks** are small pieces of content that you can place on the page.  
Examples: Search box, Login form, Recent posts, Menu.

**Regions** are areas on the page where blocks can be placed.  
Examples: Header, Sidebar, Footer, Content area.

You place blocks into regions in the Block layout page.

### 8. What are menus in Drupal?

Menus are navigation links that help users move around the website.  
Examples: Main menu, Footer menu, User account menu.  

You can create custom menus and add links to pages, nodes, or external URLs.

### 9. What is the difference between a module and a theme?

| Module | Theme |
|--------|-------|
| Adds functionality (features) | Controls the look and design |
| Written in PHP (mostly) | Uses Twig templates, CSS, JS |
| Example: Views, Pathauto | Example: Olivero, custom theme |

Modules = what the site can do.  
Themes = how the site looks.

### 10. What are contributed modules and custom modules?

- **Contributed modules**: Modules made by the Drupal community and available on drupal.org. Anyone can download and use them (example: Pathauto, Token, Webform).

- **Custom modules**: Modules you write yourself for special needs of your project. They live in the `modules/custom` folder.
