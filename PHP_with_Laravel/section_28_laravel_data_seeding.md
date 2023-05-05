# Insights on this Section
#### Seeders:
- the ability to seed your database with data using seed classes. All seed classes are stored in the database/seeders directory. By default, a DatabaseSeeder class is defined for you.
> ###### to create a seeder in terminal:
```php
php artisan make:seeder UsersTableSeeder
```
`in UsersTableSeeder`
```php
public function run(): void
{
    //
    DB::table('users')->insert([
        'name'=>Str::random(10),
        'email'=>Str::random(10).'@test.com',
        'password'=>Hash::make('secret'),
    ]);
}
```
`to seed data in db`
```php
php artisan db:seed
```
#### Factory:
- are classes that extend Laravel's base factory class and define a definition method.
> ###### to create a factory for an extending class in terminal:
```php
php artisan make:factory PostFactory --model=Post
```
`in PostFactory.php`
```php
 public function definition(): array
{
    return [
        //
        'user_id' => User::factory(),
        'title' => fake()->sentence(7, 11),
        'content' => fake()->paragraphs(rand(10, 15), true)
    ];
}
```
`in UserFactory.php`
```php
public function definition(): array
{
    return [
        'name' => fake()->name(),
        'email' => fake()->unique()->safeEmail(),
        'email_verified_at' => now(),
        'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi', // password
        'remember_token' => Str::random(10),
    ];
}
```
`in DatabaseSeeder.php`
```php
public function run(): void
{
    // \App\Models\User::factory(10)->create();

    // \App\Models\User::factory()->create([
    //     'name' => 'Test User',
    //     'email' => 'test@example.com',
    // ]);

    // $this->call(UsersTableSeeder::class);

    // factory(App\Models\User::class, 10)->create()->each(function($user) {
    //     $user->posts()->save(factory(App\Models\Post::class)->make());
    // });

    DB::statement('SET FOREIGN_KEY_CHECKS=0');
    DB::table('users')->truncate();
    DB::table('posts')->truncate();

    User::factory(3)->create()->each(function ($user) {
        $user->posts()->save(Post::factory()->make());
    });

    // Post::factory(10)->create();
}
```
