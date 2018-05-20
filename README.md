# make-observer-command
Make observer command for Laravel's artisan
## Installation
First as far as this functionality is in dev mode you need to add **minimum-stablity** and **prefer-stable** to your **composer.json** file under the config.
```json
"config": {
    "preferred-install": "dist",
    "sort-packages": true,
    "optimize-autoloader": true
  },
"minimum-stability": "dev",
"prefer-stable": true
```
Next install package via **composer**.

```bash
$ composer require nicksynev/make-observer-command
```
Then add service provider into your **app.php** file in **config** folder.
```php
NickSynev\MakeObserverCommand\MakeObserverCommandServiceProvider::class,
```
To add observer class you need to enter name, relative model's namespace and methods(optional). It will create Observers folder (if you dont have one) in your app directory and put class there. Also supports **subfolder structure** (for example User/UserObserver).
```bash
$ php artisan make:observer UserObserver 'App\Models\User' --methods=created,updated
```
There are 6 methods in command: **creating, created, updating, updated, deleting, deleted**.

If no method chosen puts all of them to a class.

Do not forget to init your observer for example in **AppServiceProvider** boot method.

```php
public function boot()
{
    User::observe(UserObserver::class);
    // Your code
}
```
When deleting package first remove service provider from **app.php**, then simply remove by composer: 
```bash
$ composer remove nicksynev/make-observer-command
```
