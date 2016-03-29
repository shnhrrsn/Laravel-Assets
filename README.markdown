# Laravel Assets

This package provides a simpler alternative to using gulp/elixir in L5.  It’s designed to get out of your way and allow you to work without worrying about running a watch command and waiting for files to compile.  All you’ll need to do is store your assets in /resources/assets, and the package will automatically detect changes and compile (and cache) on page load.

In production environments, you should run the `assets:publish` command to precompile all assets and move them into the public directory where your web server can more effeciently serve them.

## Installation

##### Add the package to composer

```bash
composer require "shnhrrsn/laravel-assets" "dev-master"
```

##### Add the following line to your service providers in `config/app.php`

```php
		Assets\ServiceProvider::class,
```

##### *(Optional)* Update your `.gitignore` files to ignore published assets

All of your assets should live in `/resources/assets`, so it’s a good idea to update your `.gitignore` to make sure published assets don’t accidentally make their way into git.

```bash
echo "published_assets.php" >> config/.gitignore
echo "css/" >> public/.gitignore
echo "img/" >> public/.gitignore
echo "js/" >> public/.gitignore
echo "font/" >> public/.gitignore
```

##### *(Optional)* Publish config

If you want to override the default config settings for Assets, you should publish the config file:

```bash
php artisan vendor:publish
```

##### Install toolchain

To quickly install the necessary tools for Assets to compile, use the built in `install-toolchain` command:

```bash
php artisan assets:install-toolchain
```

## Usage

##### Include your assets in blade via the `asset_path()` function

`asset_path()` will look for your files in `/resources/assets`, so the file referenced in the snippet below should be in `/resources/assets/scss/site.scss`.

```php
<link type="text/css" rel="stylesheet" href="{!! asset_path('scss/site.scss') !!}" />
```

Now refresh the page to make sure your file was included and properly compiled.

##### On deploy, run `php artisan assets:publish`

This will pre-compile all assets and move them into the `public/` directory.  As long as you’re using `asset_path()` to reference your assets, they’ll start serving the compiled versions.

#### Images and Fonts

Files stored in `/resources/assets/img`, `/resources/assets/font` and `/resources/assets/css` are served as-is (with proper content types) and are copied directly into the same directories in `/public` during `assets:publish`.

CSS minification is not supported at this time for raw files.  Minification is provided for scss, less, coffee and js files via their compilers.

## TODO

* Add minification support for raw css files.
