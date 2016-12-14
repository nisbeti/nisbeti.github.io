---
layout: post
title: Selenium Testing Laravel Spark
date: 2016-12-02
---

It almost feels like a waste of time, now that Taylor tweeted a hint that he'd integrate Selenium testing into Laravel, but in the meantime, this is what I have been doing.

First, I install the package [https://github.com/Modelizer/Selenium](https://github.com/Modelizer/Selenium) which is awsome.

Then I write a test, as follows:

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use Modelizer\Selenium\SeleniumTestCase;

class RegisterUserSeleniumTest extends SeleniumTestCase
{
    use DatabaseTransactions;
    
    public function testCanRegisterUser()
    {
        // $this->markTestSkipped();
        
        $this->visit('/register')
            ->typeInformation([
                'name' => 'Test User',
                'email' => time() . '@example.com',
                'password' => 'P12345678',
                'password_confirmation' => 'P12345678',
            ])
            ->click('terms')
            ->click('#register-button')
            ->hold(6)
            ->see('Dashboard');
    }
}
```

Run PHPUnit as normal;

Green!
