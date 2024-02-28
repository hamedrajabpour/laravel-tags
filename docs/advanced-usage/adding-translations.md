---
title: Adding translations
weight: 1
---

When using the package like described in the basic usage section all tags will be stored in the locale your app is running. If you're creating a multilingual app it's really easy to translate the tags. Here's a quick example.

```php
$tag = Tag::findOrCreate('my tag'); //store in the current locale of your app

//don't forget to save the model
$tag->save();

$tag->name // returns the name of the tag in current locale of your app.
```

