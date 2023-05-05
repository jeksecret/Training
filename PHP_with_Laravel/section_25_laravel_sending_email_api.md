# Insights on this Section
#### Setting up Mailgun:
> ###### visit the site and create a free account:
https://www.mailgun.com/
> ###### install client in terminal:
```php
composer require symfony/mailgun-mailer symfony/http-client
```
#### Configuration:
> ###### get the domain and secret key from your mailgun account:
`in .env file`
```php
MAIL_MAILER=mailgun
MAILGUN_DOMAIN=sandbox29fba16d8604411bbca9d0369a27489e.mailgun.org
MAILGUN_SECRET=4a7944c73861c9bf112114ea9479323c-102c75d8-a782ef7c
```
`in config/mail.php`
```php
'from' => [
    // 'address' => env('MAIL_FROM_ADDRESS', 'hello@example.com'),
    'address' => env('MAIL_FROM_ADDRESS', 'jake.bontilao@nabepero.co.jp'),
    // 'name' => env('MAIL_FROM_NAME', 'Example'),
    'name' => env('MAIL_FROM_NAME', 'Jake'),
],
```
`creating route in web.php`
```php
Route::get('/sendmail', function () {
    $data = [
        'title'=>'PHP',
        'content'=>'PHP with Laravel'
    ];

    Mail::send('email.test', $data, function ($message) {
        // $message->from('john@johndoe.com', 'John Doe');
        // $message->sender('john@johndoe.com', 'John Doe');
        $message->to('jake.bontilao@gmail.com', 'Jake Bontilao');
        // $message->cc('john@johndoe.com', 'John Doe');
        // $message->bcc('john@johndoe.com', 'John Doe');
        // $message->replyTo('john@johndoe.com', 'John Doe');
        $message->subject('Udemy Course');
        // $message->priority(3);
        // $message->attach('pathToFile');
    });
});
```
