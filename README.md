# Add tags and taggable behaviour to a Laravel app

[![Latest Version on Packagist](https://img.shields.io/packagist/v/hamedrajabpour/laravel-tags.svg?style=flat-square)](https://packagist.org/packages/hamedrajabpour/laravel-tags)
[![MIT Licensed](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
![GitHub Workflow Status](https://img.shields.io/github/workflow/status/hamedrajabpour/laravel-tags/run-tests?label=tests)
[![Total Downloads](https://img.shields.io/packagist/dt/hamedrajabpour/laravel-tags.svg?style=flat-square)](https://packagist.org/packages/hamedrajabpour/laravel-tags)

This package offers taggable behaviour for your models. After the package is installed the only thing you have to do is add the `HasTags` trait to an Eloquent model to make it taggable. 

The Main Diffrence Between This Package & Spatie that removed translation & slug

Here are some code examples:

```php
// apply HasTags trait to a model
use Illuminate\Database\Eloquent\Model;
use Spatie\Tags\HasTags;

class NewsItem extends Model
{
    use HasTags;
    
    // ...
}
```

```php

// create a model with some tags
$newsItem = NewsItem::create([
   'name' => 'The Article Title',
   'tags' => ['first tag', 'second tag'], //tags will be created if they don't exist
]);

// attaching tags
$newsItem->attachTag('third tag');
$newsItem->attachTag('third tag','some_type');
$newsItem->attachTags(['fourth tag', 'fifth tag']);
$newsItem->attachTags(['fourth_tag','fifth_tag'],'some_type');

// detaching tags
$newsItem->detachTag('third tag');
$newsItem->detachTag('third tag','some_type');
$newsItem->detachTags(['fourth tag', 'fifth tag']);
$newsItem->detachTags(['fourth tag', 'fifth tag'],'some_type');

// get all tags of a model
$newsItem->tags;

// syncing tags
$newsItem->syncTags(['first tag', 'second tag']); // all other tags on this model will be detached

// syncing tags with a type
$newsItem->syncTagsWithType(['category 1', 'category 2'], 'categories'); 
$newsItem->syncTagsWithType(['topic 1', 'topic 2'], 'topics'); 

// retrieving tags with a type
$newsItem->tagsWithType('categories'); 
$newsItem->tagsWithType('topics'); 

// retrieving models that have any of the given tags
NewsItem::withAnyTags(['first tag', 'second tag'])->get();

// retrieve models that have all of the given tags
NewsItem::withAllTags(['first tag', 'second tag'])->get();

// retrieve models that don't have any of the given tags
NewsItem::withoutTags(['first tag', 'second tag'])->get();


// using tag types
$tag = Tag::findOrCreate('tag 1', 'my type');


// tags are sortable
$tag = Tag::findOrCreate('my tag');
$tag->order_column; //returns 1
$tag2 = Tag::findOrCreate('another tag');
$tag2->order_column; //returns 2

// manipulating the order of tags
$tag->swapOrder($anotherTag);
```


## Requirements

This package requires Laravel 8 or higher, PHP 8 or higher, and a database that supports `json` fields and MySQL compatible functions.

## Installation

You can install the package via composer:

``` bash
composer require hamedrajabpour/laravel-tags
```

The package will automatically register itself.

You can publish the migration with:
```bash
php artisan vendor:publish --provider="Spatie\Tags\TagsServiceProvider" --tag="tags-migrations"
```

After the migration has been published you can create the `tags` and `taggables` tables by running the migrations:

```bash
php artisan migrate
```

You can optionally publish the config file with:
```bash
php artisan vendor:publish --provider="Spatie\Tags\TagsServiceProvider" --tag="tags-config"
```



## Testing

1. Copy `phpunit.xml.dist` to `phpunit.xml` and fill in your database credentials.
2. Run `composer test`.




## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
