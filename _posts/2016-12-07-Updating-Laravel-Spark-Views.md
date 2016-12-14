---
title: Updating Laravel Spark Views
---

Before Composer Update:

```
cp -r vendor/laravel/spark/resources/views resources/before_composer_update/vendor/laravel/spark/resources/views
cp -r vendor/laravel/spark/install-stubs/resources/assets resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/assets
cp -r vendor/laravel/spark/install-stubs/resources/lang resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/lang
diff -rw resources/before_composer_update/vendor/laravel/spark/resources/views/ resources/views/vendor/spark > resources/before_composer_update/views-modified.diff
diff -rw resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/assets/ resources/assets > resources/before_composer_update/assets-modified.diff
diff -rw resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/lang/ resources/lang > resources/before_composer_update/lang-modified.diff
```

```composer update```

```
diff -rw resources/before_composer_update/vendor/laravel/spark/resources/views vendor/laravel/spark/resources/views/ > resources/after_composer_update/views-changed.diff
diff -rw resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/assets/ vendor/laravel/spark/install-stubs/resources/assets/ > resources/after_composer_update/assets-changed.diff
diff -rw resources/before_composer_update/vendor/laravel/spark/install-stubs/resources/lang/ vendor/laravel/spark/install-stubs/resources/lang/ > resources/after_composer_update/lang-changed.diff
diff -rw vendor/laravel/spark/resources/views/ resources/views/vendor/spark/ > resources/after_composer_update/views-to-update.diff
diff -rw vendor/laravel/spark/install-stubs/resources/assets/ resources/assets/ > resources/after_composer_update/assets-to-update.diff
diff -rw vendor/laravel/spark/install-stubs/resources/lang/ resources/lang/ > resources/after_composer_update/lang-to-update.diff
```
