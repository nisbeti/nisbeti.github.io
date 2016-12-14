---
title: Testing Laravel Resource Controllers
---
When testing a Laravel Resource Controller, here are a few tips.

Consider a Users Controller

The ```store``` route should be protected (either by middleware or a Form Request, so that only authorized users can create new users. The ```create``` route should also be protected, so that the form to create new users is not accessible to unauthorized users. Therefore, the following ```visit()``` method will not work, as the unauthorized user is redirected away from the form.

```php
public function testUnauthorizedUserCannotAddUser()
    {      
        $user = factory(App\User::class)->create();
        $user->assignRole('authorized_user');
        
        $this->actingAs($user)
            ->visit('users/create')
            ->type('john', 'name')
            ->type('john@example.com', 'email')
            ->press('create-account')
            ->assertResponseStatus('403');
    }
```

Even if the ```create``` route was not protected; only the ```store``` route was, the above would still not work, as the ```visit()``` method checks for a 200 response, but does not receive one, so the test fails with the following message ```A request to [http://localhost/users] failed. Received status code [403].```

The solution is to test posting directly to the ```store``` route, and keep the test to check that an unauthorized user cannot access the ```create``` route in a seperate test, using the ```get()``` method.

```php
public function testUnauthorizedUserCannotAddUser()
    {      
        $user = factory(App\User::class)->create();
        $user->assignRole('unauthorized_user');
        
        $this->actingAs($user)
            ->post('users', [
                'name' => 'john',
                'email' => 'john@example.com'
            ])
            ->assertResponseStatus('403');
    }
```

and 

```php
    public function testUnauthorizedUserCannotViewAddUserForm()
    {
        // $this->markTestSkipped();
        
        $user = factory(App\User::class)->create();
        $user->assignRole('unauthorized_user');
        
        $this->actingAs($user)
            ->get('users/create')
            ->assertResponseStatus('403');
    }
```
