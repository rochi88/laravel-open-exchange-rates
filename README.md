# laravel-open-exchange-rates

This package provides a simple and convenient interface for working with the Open Exchange Rates service. Currently supports free endpoints.
### Installation Via Composer

Add this to your `composer.json` file, in the require object:
```sh
"rochi88/laravel-open-exchange-rates": "dev-main"
```
After that, run `composer install` to install the package.

Lastly, publish the config file.

```sh
php artisan vendor:publish --provider="Rochi88\LaravelOpenExchangeRates\LOERServiceProvider"
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
use Rochi88\LaravelOpenExchangeRates\Client;

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
