## PHP  


### Basic Syntax
  
##### Variables  
* Variable Declaration  
```php  
$variable_name = value;  
```  
  
* Variable Types  
```php  
$integer_variable = 42;  
$float_variable = 3.14;  
$string_variable = "Hello, World!";  
$boolean_variable = true;  
$array_variable = array(1, 2, 3);  
$null_variable = null;  
```  
  
- - -  
  
##### Control Structures  
* If Statement  
```php  
if (condition) {  
    // code to execute if condition is true  
} elseif (condition2) {  
    // code to execute if condition2 is true  
} else {  
    // code to execute if all conditions are false  
}  
```  
  
* Switch Statement  
```php  
switch ($variable) {  
    case value1:  
        // code to execute if $variable equals value1  
        break;  
    case value2:  
        // code to execute if $variable equals value2  
        break;  
    default:  
        // code to execute if $variable doesn't match any case  
        break;  
}  
```  
  
* For Loop  
```php  
for ($i = 0; $i < 5; $i++) {  
    // code to execute repeatedly  
}  
```  
  
* While Loop  
```php  
while (condition) {  
    // code to execute repeatedly as long as condition is true  
}  
```  
  
* Do-While Loop  
```php  
do {  
    // code to execute repeatedly at least once  
} while (condition);  
```  
  
- - -  
  
##### Functions  
* Function Declaration  
```php  
function function_name($param1, $param2) {  
    // code to execute  
}  
```  
  
* Function Call  
```php  
function_name($arg1, $arg2);  
```  
  
- - -  
  
##### Arrays  
* Indexed Array  
```php  
$indexed_array = array("apple", "banana", "cherry");  
```  
  
* Associative Array  
```php  
$associative_array = array("name" => "John", "age" => 25, "city" => "New York");  
```  
  
* Accessing Array Elements  
```php  
$indexed_array[0];  // returns "apple"  
$associative_array["name"];  // returns "John"  
```  
  
- - -  
  
##### Strings  
* String Concatenation  
```  
$greeting = "Hello";  
$name = "John";  
$full_greeting = $greeting . ", " . $name . "!";  
```  
  
* String Length  
```php  
$length = strlen($string);  
```  
  
* Substring  
```php  
$substring = substr($string, $start, $length);  
```  
  
- - -  
  
##### File Handling  
* Read File  
```php  
$file_content = file_get_contents($file_path);  
```  
  
* Write to File  
```php  
file_put_contents($file_path, $data);  
```  
  
- - -  
  
### Laravel  
  
##### Routing  
* Basic Routing  
```php  
Route::get('/url', 'Controller@method');  
```  
  
* Route Parameters  
```php  
Route::get('/user/{id}', 'UserController@show');  
```  
  
* Route Names  
```php  
Route::get('/url', 'Controller@method')->name('route.name');  
```  
  
- - -  
  
##### Controllers  
* Creating a Controller  
```bash  
$ php artisan make:controller ControllerName  
```  
  
* Controller Methods  
```php  
public function methodName(Request $request)  
{  
    // code to execute  
    return response()->json($data);  
}  
```  
  
- - -  
  
##### Models  
* Creating a Model  
  
```bash  
$ php artisan make:model ModelName  
```  
  
* Model Relationships  
```php  
public function relatedModel()  
{  
    return $this->belongsTo(RelatedModel::class);  
}  
```  
  
- - -  
  
##### Migrations  
* Creating a Migration  
```bash  
$ php artisan make:migration create_table_name  
```  
  
* Running Migrations  
  
```bash  
$ php artisan migrate  
```  
  
- - -  
  
##### Views  
* Blade Templates  
```html  
@extends('layout')  
@section('content')  
    // code to display content  
@endsection  
```  
  
* Passing Data to Views  
```php  
return view('view_name', ['data' => $data]);  
```  
  
- - -  
  
##### Eloquent ORM  
* Retrieving Data  
```php  
$users = User::all();  
```  
  
* Creating a New Record  
```php  
$user = new User;  
$user->name = 'John';  
$user->email = 'john@example.com';  
$user->save();  
```  
  
* Updating a Record  
```php  
$user = User::find($id);  
$user->name = 'New Name';  
$user->save();  
```  
  
* Deleting a Record  
```php  
$user = User::find($id);  
$user->delete();  
```  
  
- - -  
  
##### Middleware  
* Creating Middleware  
```bash  
php artisan make:middleware MiddlewareName  
```  
  
* Applying Middleware  
```php  
Route::get('/url', 'Controller@method')->middleware('middleware_name');  
```  
  
- - -  
  
##### Authentication  
* User Registration  
```php  
use Illuminate\Support\Facades\Hash;  
  
public function register(Request $request)  
{  
    $user = new User;  
    $user->name = $request->name;  
    $user->email = $request->email;  
    $user->password = Hash::make($request->password);  
    $user->save();  
}  
```  
  
* User Login  
```php  
use Illuminate\Support\Facades\Auth;  
  
public function login(Request $request)  
{  
    $credentials = $request->only('email', 'password');  
    if (Auth::attempt($credentials)) {  
        // Authentication passed  
    }  
}  
```  
