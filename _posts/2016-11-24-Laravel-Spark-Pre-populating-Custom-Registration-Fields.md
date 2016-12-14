---
layout: default
title: Laravel Spark - Pre-populating Custom Registration Fields
---
The Laravel Spark <a href="https://spark.laravel.com/docs/3.0/adding-registration-fields" target="_blank">documentation</a> explains how to add additional registration fields.

I wanted to add a <strong>role</strong> field to my registration form. Following the docs:

<code><input type="text" class="form-control" name="role" v-model="registerForm.role"></code>

If left at that, the new fields will appear on the page, but the <code>input</code> tag cannot simply be pre-populated with <code>value="some value"</code>.

Following the docs again, in the <code>/resources/assets/js/app.js</code> file, I added the following lines of code just before the call to <code>new Vue</code>:

<pre><code>Spark.forms.register = {
    role: ''
};

var app = new Vue({
    mixins: [require('spark')]
});</code></pre>

If I put a value into <code>role: 'staff'</code>, for example, then the field is pre-populated, but fixed.

<h3>What if I want to pre-populate with some value from a database, for example?</h3>

To do this, I went back and undid the previous changes to <code>/resources/assets/js/app.js</code>, then I created a new Register data object on the page (as I did not want to add it to the spark global state object). I changed <code>/resources/assets/js/spark-components/auth/register-stripe.js</code> to the following:

<pre><code>
    props: [],
    
    data() {
        return {
            registerForm: {
                role: Register.role
            }
        };
    },
    
    mixins: [base]</code></pre>

As my new Data object is to be called Register.

Finally, to give the dynamic data to the template and set up the Register data object, I amended the <code>/resources/views/vendor/spark/auth/register-stripe.blade.php</code> file as follows:

<pre><code>
@section('scripts')
    <script src="https://js.stripe.com/v2/"></script>
    <script>
        window.Register = <?php echo json_encode([
            'role' => $role
        ]); ?>;
    <script>
@endsection

@section('content')
<spark-register-stripe inline-template>
</code></pre>

The last part was using a View Composer to make the <code>$role</code> data available to the view.

<pre><code><?php

namespace App\Http\ViewComposers;

use Illuminate\View\View;
use Illuminate\Http\Request;
use App\Repositories\UserRepository;

class ShowRegistrationFormComposer
{
    /**
     * Create a new profile composer.
     *
     * @param  Request  $request
     * @return void
     */
    public function __construct(Request $request)
    {
        $this->request = $request;
    }
    
    /**
     * Bind data to the view.
     *
     * @param  View  $view
     * @return void
     */
    public function compose(View $view)
    {
        $role = $this->request->role ?: 'parent';
        
        $view->with('role', $role);
    }
}</code></pre>

and

<pre><code><?php

namespace App\Providers;

use Illuminate\Support\Facades\View;
use Illuminate\Support\ServiceProvider;

class ComposerServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap the application services.
     *
     * @return void
     */
    public function boot()
    {
        View::composer(
            'spark::auth.register', 'App\Http\ViewComposers\ShowRegistrationFormComposer'
        );
    }

    /**
     * Register the application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}
</code></pre>
