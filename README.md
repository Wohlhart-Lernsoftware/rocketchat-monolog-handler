# [Rocket.chat](https://rocket.chat/) Monolog Handler by Sysvale

![Monolog Handler CI](https://github.com/Sysvale/rocketchat-monolog-handler/workflows/Monolog%20Handler%20CI/badge.svg)

Monolog Handler para ser usado em projetos Laravel. Adaptado da implementação para Slack.

Inspirado nos seguintes projetos:
 - https://github.com/beeproger/rocketchat-monolog-handler

 - https://github.com/martinusso/monolog-rocketchat-handler

## Instalação

```bash
composer require sysvale/rocketchat-monolog-handler
```

## Uso

Importe a seguinte classe no seu `config/logging.php`

```php
use Sysvale\Logging\RocketChatHandler;
```

Adicione o código abaixo ao Array de `channels` no arquivo `logging.php`

```php
'rocketchat' => [
    'driver' => 'monolog',
    'handler' => RocketChatHandler::class,
    'with' => [
        'webhooks' => [env('ROCKET_CHAT_WEBHOOK', '')],
        'username' => 'Awesome Laravel Bot',
        'emoji' => ':rotating_light:',
    ],
    'level' => 'warning',
],
```

Atualize o canal `stack` de:

```php
'channels' => ['daily'],
```

para:

```php
'channels' => ['daily', 'rocketchat'],
```

Lembre-se de adicionar as variáveis de ambiente

```
ROCKET_CHAT_WEBHOOK=
```

[Configure um WebHook](https://rocket.chat/docs/administrator-guides/integrations/) no seu servidor do Rocket.Chat

Você pode utilizar o seguinte script:

```javascript
/* exported Script */
/* globals console, _, s */

/** Global Helpers
 *
 * console - A normal console instance
 * _       - An underscore instance
 * s       - An underscore string instance
 */

class Script {
  /**
   * @params {object} request
   */
  process_incoming_request({ request }) {

    // console is a global helper to improve debug
    console.log(request);

    return {
      content:{
        text: request.content.text,
        username: request.content.username,
        emoji: request.content.emoji,
        attachments: request.content.attachments
       }
    };
  }
}
```
