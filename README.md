# php-gpt-client

Just a small php client to interact with gpt-stuff

## Caution

This is a very early version of this client. It is not tested and not ready for production. Use at your own risk.
It is also not complete. It is just a small client to interact with the gpt-3 api.
It is not a full-featured client for the whole openai api.
It is also not an official client.

## Requirements

- PHP 8.1 or higher

## Installation

```bash
composer require teevee/php-gpt-client
```

## Usage

### ask for models

```php
<?php
declare(strict_types=1);

require dirname(__DIR__) . '/vendor/autoload.php';

use TeeV\GptClient\Api\Gpt;
use TeeV\GptClient\HttpClient\ConnectionException;

try {
  $client = new Gpt('sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx');
  $result = $client->getModels();
  var_dump($result);
} catch (ConnectionException $e) {
  echo 'Error: ', $e->getMessage(), PHP_EOL;
}
```

### ask for completions

```php
<?php
declare(strict_types=1);

require dirname(__DIR__) . '/vendor/autoload.php';

use TeeV\GptClient\Api\ChatParams;
use TeeV\GptClient\Api\Gpt;
use TeeV\GptClient\Api\Message;
use TeeV\GptClient\Api\Role;
use TeeV\GptClient\HttpClient\ConnectionException;

try {
  $client = new Gpt('sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx');
  $result = $client->chat(
    new ChatParams(
      'gpt-3.5-turbo',
      [
        (new Message(
          Role::USER,
          'How are you?',
          'random guy'
        ))->getMessage(),
      ]
    )
  );

  var_dump($result);
} catch (ConnectionException $e) {
  echo 'Error: ', $e->getMessage(), PHP_EOL;
}