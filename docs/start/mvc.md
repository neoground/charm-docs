---
key:     start.mvc
title:   Models, Views & Controllers
section: Getting Started
nav:
  prev:
    page: start.structure
    icon: prev
    name: Structure
  next:
    page: start.magnet
    icon: next
    name: Magic Magnet
---

# ->> Models, Views & Controllers <<-

<div class="card card-body" markdown="1">

In our framework, the architectural pattern of Model-View-Controller (MVC) lays the foundation for 
orchestrating a clean separation of concerns among the data, the presentation, and the actions
taken based on user interactions. The Model encapsulates the core data logic, the View renders
the user interface and presents the data,
while the Controller acts as an intermediary that handles the input from the user, 
processes it (with possible updates to the Model), and returns the output display (View) or a different Response
type, like JSON or a File. 
This trifecta harmonizes the codebase, promoting organized, scalable, and maintainable code. 
As you delve into the sections below, a deeper understanding of each component and their 
interplay within our framework will unfold.
</div>

## ->> Models

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/models.jpg" alt="Section Heading Image" /></div>

They are found here: `app/Models`.

You can easily use them to represent database tables. Models are based on the Laravel models, 
so the functionality is also very similar. They are also used for simple access to a database table,
thanks to the Eloquent system.

### -> Sample model

Includes an optional simple table migration.

```php
namespace App\Models;

use Charm\Vivid\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class User extends Model
{
    protected $table = 'users';

    protected $fillable = ['id', 'username', 'email'];

    protected $casts = [
        'favorite_artists' => 'array'
    ];

    use SoftDeletes;

    public static function getTableStructure(): \Closure
    {
        return function(Blueprint $table) {
            $table->increments('id');

            $table->string('username');
            $table->string('password')
            $table->string('email')
            $table->string('favorite_icecream')->nullable();
            $table->tinyInteger('age');
            $table->string('favorite_artists')->nullable();

            $table->timestamps();
            $table->softDeletes();
        };
    }

    public function getDisplayName() : string
    {
        return $this->username;
    }

}
```
</div>

## ->> Views

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/views.jpg" alt="Section Heading Image" /></div>

They are found here: `app/Views`.

Views are based on [twig views](https://twig.symfony.com/). 
They are easy to use and you can create awesome views with them.

In a controller you will return a view. Variables can be passed there. 
The naming scheme is the usual dot-notation. A view called by 
`return View::make('pages.static.legal')->(...)` will be found at `app/Views/pages/static/legal.twig`.
</div>


## ->> Controllers

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/controllers.jpg" alt="Section Heading Image" /></div>

They are found here: `app/Controllers`.

Your main application logic is found in the controllers. Here are all methods found which are executed by routes / API.

You define the route by a simple attribute. For advances routing see the Routing section.

### -> Sample controller

```php
namespace App\Controllers;

use Charm\Vivid\C;
use Charm\Vivid\Controller;
use Charm\Vivid\Kernel\Output\View;
use Charm\Vivid\Router\Attributes\Route;

class BasicController extends Controller
{
    #[Route("GET", "/demo", "basic.index")]
    public function getIndex()
    {
        $name = C::Request()->get('name', 'Rudi');
        return View::make('index')->with([
            'foo' => 'bar',
            'name' => $name
        ]);
    }
}
```

In this example the route `/demo` with the name `basic.index` will call `getIndex()`, 
which will display the view index. The view file is `app/Views/index.twig`. 
If you call this page with the GET parameter `?name=John`, the variable
`name` in the view will be John and not Rudi (default value).

</div>


## ->> Intelligent filters and queries for a model

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/filters.jpg" alt="Section Heading Image" /></div>

You can easily define attributes which are available for filtering and querying inside the model:

```php
namespace App\Models;

use Charm\Vivid\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class User extends Model
{
    protected $table = 'users';

    protected $fillable = ['id'];

    protected $casts = [
        'favorite_artists' => 'array'
    ];

    protected $filter_attributes = [
        'username' => 'string_like',
        'email' => 'string',
        'favorite_icecream' => 'string_like',
        'age' => 'range',
        'favorite_artists' => 'array'
    ];

    protected $search_attributes = [
        'username',
        'email'
    ];

    use SoftDeletes;

    public function formatToArray()
    {
        return [
            'id' => $this->id,
            'title' => $this->title,
            'created' => $this->created_at
        ];
    }
}
```

This example also includes the formatting of the values to an array which will be added to the returned data. If this method is not available, the built-in toArray() method will be used.

The controller is fairly short and looks like this to support the filtering:

```php
namespace App\Controllers;

use App\Models\User;
use Charm\Vivid\Controller;
use Charm\Vivid\Kernel\Output\Json;
use Charm\Vivid\Router\Attributes\Route;

class BasicController extends Controller
{
    #[Route("GET", "/", "basic.index")]
    public function getIndex()
    {
        return Json::make(User::getFilteredPaginatedData());
    }
}
```

You can then filter by adding this to the URL: `?username=duke`

These types of filter attributes are available:

- `string` (simple WHERE search)
- `string_like` (like search, automatically adds "%")
- `range` (provide values as from;to or in separate fields name_from and name_to. Will result in: WHERE field BETWEEN from AND to)
- `array` (WHERE IN array)

- Further explanation of "range": you can easily use this and only provide a "from" or "to" value. For example if only name_to is set, the query would be WHERE field <= to. Is only name_from set, the query would be WHERE field => name_from.

You can also add `?order_by=field&order_dir=ASC` to change the order.
`order_dir` must be ASC or DESC. The direction can also be provided by appending `_ASC` or `_DESC` 
to the end of order_by.

The JSON result will look like this. Inside the data array are objects of all entities,
formatted like described in `formatToArray()`.

```php
{
    "total": 404,
    "per_page": 25,
    "current_page": 1,
    "last_page": 17,
    "first_page_url": "https://example.com/demo?page=1",
    "last_page_url": "https://example.com/demo?page=17",
    "next_page_url": "https://example.com/demo?page=2",
    "prev_page_url": null,
    "data": [...]
}
```

</div>