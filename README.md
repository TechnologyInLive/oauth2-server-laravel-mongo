# PHP OAuth 2.0 Server for Laravel and MongoDB


## Package Installation

You can install the package via composer. add the following line to your composer.json file:

```javascript
"technologyinlive/oauth-server-laravel-mongo": "dev-master"
```

Add this line of code to the ```providers``` array located in your ```app/config/app.php``` file:
```php
'LucaDegasperi\OAuth2Server\Storage\FluentStorageServiceProvider',
'LucaDegasperi\OAuth2Server\OAuth2ServerServiceProvider',
```

And this lines to the ```aliases``` array:
```php
'Authorizer' => 'LucaDegasperi\OAuth2Server\Facades\AuthorizerFacade',
```

## Manual Modifications

Change
```php
if ($userId === false) {
    $this->server->getEventEmitter()->emit(new Event\UserAuthenticationFailedEvent($this->server->getRequest()));
    throw new Exception\InvalidCredentialsException();
}     
```
to
```php
if(gettype($userId)=='array'){
    return json_encode($userId);
}else if ($userId === false) {
    $this->server->getEventEmitter()->emit(new Event\UserAuthenticationFailedEvent($this->server->getRequest()));
    throw new Exception\InvalidCredentialsException();
}
```
In **vendor/league/oauth2-server/src/Grant/PasswordGrant.php**


The code on which this package is [based](https://github.com/lucadegasperi/oauth2-server-laravel)

This is a **VERY UNSTABLE** version
