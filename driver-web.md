# Web

- [Installation & Setup](#installation-setup)
- [Supported Features](#supported-features)

<a id="installation-setup"></a>
## Installation & Setup

First you need to pull in the Web Driver.

```sh
composer require botman/driver-web
```

Then load the driver before creating the BotMan instance (**only when you don't use BotMan Studio**):

```php
DriverManager::loadDriver(\BotMan\Drivers\Web\WebDriver::class);

// Create BotMan instance
BotManFactory::create($config);
```

Or if you use BotMan Studio:

```sh
php artisan botman:install-driver web
```

This driver can be used as a starting point to add BotMan to your website or API. The driver itself receives the incoming requests and responds with a JSON representing the message result. So you can for example build your own chat-interface that talks to BotMan through the WebDriver.

### Example incoming request

This is a basic and valid incoming JSON request for the WebDriver. In BotMan Studio it works as GET or POST request, but it depends on your BotMan setup.

```json
{
	"driver": "web",
	"userId": "1234",
	"message": "hi"
}
```

The `driver` value is used to validate the request for this specific driver. Read more about that below. The `userId` is the sender of the request and used for connecting requests to conversations. And finally the `message` is the content of the user's message obviously. 

> {callout-info} You can send more values along the request and use them in you application as well.

### Example Response
This is an example response from BotMan. It contains a `message` array that holds all messages that BotMan replies.

```json
{
    "status":200,
    "messages":[
        {
            "type":"text",
            "text":"I have no idea what you are talking about!",
            "attachment":{
                "type":"image",
                "url":"https:\/\/botman.io\/img\/logo.png",
                "title":null
            }
        }
    ]
}
```
The driver configuration allows you to define which request parameters need to be present in order for BotMan to detect the incoming request as a request for the "web" driver. By default, all HTTP requests to your BotMan controller need to contain a `driver` attribute with the value `web`.
Pass the driver configuration to the `BotManFactory` upon initialization. If you use BotMan Studio, you can find the configuration file located under `config/botman/web.php`.

```php
[
    'web' => [
    	'matchingData' => [
            'driver' => 'web',
        ],
    ]
]
```

<a id="supported-features"></a>
## Supported Features
Since this is a "naked" web-driver implementation, it is up to you to implement the features that you need.
