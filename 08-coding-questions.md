# Coding Questions

All examples are written in simple form for Drupal 10/11.

### 1. Write a custom module that displays "Hello World."

**hello_world.info.yml**
```yaml
name: 'Hello World'
type: module
description: 'A simple Hello World module'
core_version_requirement: ^10 || ^11
package: Custom
```

**hello_world.routing.yml**
```yaml
hello_world.hello:
  path: '/hello-world'
  defaults:
    _controller: '\Drupal\hello_world\Controller\HelloController::content'
    _title: 'Hello World'
  requirements:
    _permission: 'access content'
```

**src/Controller/HelloController.php**
```php
<?php

namespace Drupal\hello_world\Controller;

use Drupal\Core\Controller\ControllerBase;

class HelloController extends ControllerBase {

  public function content() {
    return [
      '#markup' => $this->t('Hello World'),
    ];
  }

}
```

### 2. Create a custom route and controller

(See example above – that is exactly a custom route + controller.)

### 3. Create a custom block plugin

**src/Plugin/Block/HelloBlock.php**
```php
<?php

namespace Drupal\hello_world\Plugin\Block;

use Drupal\Core\Block\BlockBase;

/**
 * @Block(
 *   id = "hello_block",
 *   admin_label = @Translation("Hello Block")
 * )
 */
class HelloBlock extends BlockBase {

  public function build() {
    return [
      '#markup' => $this->t('Hello from custom block!'),
    ];
  }

}
```

### 4. Create a custom form using Form API

**src/Form/HelloForm.php**
```php
<?php

namespace Drupal\hello_world\Form;

use Drupal\Core\Form\FormBase;
use Drupal\Core\Form\FormStateInterface;

class HelloForm extends FormBase {

  public function getFormId() {
    return 'hello_form';
  }

  public function buildForm(array $form, FormStateInterface $form_state) {
    $form['name'] = [
      '#type' => 'textfield',
      '#title' => $this->t('Your name'),
      '#required' => TRUE,
    ];
    $form['submit'] = [
      '#type' => 'submit',
      '#value' => $this->t('Say Hello'),
    ];
    return $form;
  }

  public function submitForm(array &$form, FormStateInterface $form_state) {
    $this->messenger()->addMessage($this->t('Hello @name!', [
      '@name' => $form_state->getValue('name'),
    ]));
  }

}
```

### 5. Create a custom service

**hello_world.services.yml**
```yaml
services:
  hello_world.greeter:
    class: Drupal\hello_world\Greeter
    arguments: ['@current_user']
```

**src/Greeter.php**
```php
<?php

namespace Drupal\hello_world;

use Drupal\Core\Session\AccountProxyInterface;

class Greeter {

  protected $currentUser;

  public function __construct(AccountProxyInterface $current_user) {
    $this->currentUser = $current_user;
  }

  public function greet() {
    return 'Hello ' . $this->currentUser->getDisplayName();
  }

}
```

### 6. Create an Event Subscriber

**hello_world.services.yml** (add)
```yaml
  hello_world.event_subscriber:
    class: Drupal\hello_world\EventSubscriber\HelloSubscriber
    tags:
      - { name: event_subscriber }
```

**src/EventSubscriber/HelloSubscriber.php**
```php
<?php

namespace Drupal\hello_world\EventSubscriber;

use Symfony\Component\EventDispatcher\EventSubscriberInterface;
use Symfony\Component\HttpKernel\KernelEvents;
use Symfony\Component\HttpKernel\Event\RequestEvent;

class HelloSubscriber implements EventSubscriberInterface {

  public static function getSubscribedEvents() {
    return [
      KernelEvents::REQUEST => 'onRequest',
    ];
  }

  public function onRequest(RequestEvent $event) {
    // Your code here
  }

}
```

### 7. Create a custom Twig filter

**hello_world.services.yml**
```yaml
  hello_world.twig_extension:
    class: Drupal\hello_world\Twig\HelloTwigExtension
    tags:
      - { name: twig.extension }
```

**src/Twig/HelloTwigExtension.php**
```php
<?php

namespace Drupal\hello_world\Twig;

use Twig\Extension\AbstractExtension;
use Twig\TwigFilter;

class HelloTwigExtension extends AbstractExtension {

  public function getFilters() {
    return [
      new TwigFilter('hello_upper', [$this, 'helloUpper']),
    ];
  }

  public function helloUpper($string) {
    return strtoupper($string);
  }

}
```

Usage in Twig: `{{ 'hello'|hello_upper }}`

### 8. Write a database query using Drupal's Database API

```php
$database = \Drupal::database();

// Select
$result = $database->select('node_field_data', 'n')
  ->fields('n', ['nid', 'title'])
  ->condition('type', 'article')
  ->condition('status', 1)
  ->range(0, 10)
  ->execute()
  ->fetchAll();

// Insert
$database->insert('my_table')
  ->fields(['name' => 'John', 'age' => 30])
  ->execute();
```

### 9. Create a custom permission

**hello_world.permissions.yml**
```yaml
access hello world page:
  title: 'Access Hello World page'
  description: 'Allow users to see the Hello World page'
```

Then use it in routing:
```yaml
requirements:
  _permission: 'access hello world page'
```
