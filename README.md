# laravel-open-exchange-rates

This package provides a simple and convenient interface for working with the Open Exchange Rates service. Currently supports free endpoints.
### Installation Via Composer

Add this to your `composer.json` file, in the require object:
```sh
"equentor/laravel-open-exchange-rates": "dev-master"
```
After that, run `composer install` to install the package.
Add the service provider to `app/config/app.php`, within the providers array:
```php
'providers' => [
    // ...
    Equentor\LaravelOpenExchangeRates\LOERServiceProvider::class,
]
```
Lastly, publish the config file.

```sh
php artisan vendor:publish
```
### Usage example
In `config/loer.php`
```php
return [
    'app_id' => '*****************************', // your own api key
    'default_base_currency' => 'USD'
];
```
In controller (or service) method:
```php
use Equentor\LaravelOpenExchangeRates\Client;

class SomeController extends Controller
{
    private $client;
    
    public function __construct(Client $client)
    {
        $this->client = $client;
    }
    
    public function someAction()
    {
        $coefficient = $this->client->latest('USD,RUB,AWG');
        
        $historical_coefficent $this->client->historical('2011-03-05', 'USD,RUB,AWG');
        
        // e.t.c...
        
        // Change in base currencies (not allowed for free account) and requests for the coefficients of all currencies relative to.
        $coefficient = $this->client->currency('RUB')->latest();
    }
}
```
