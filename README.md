# Laravel API Test with Sanctum Authentication

> Simple demonstration on sanctum authentication in laravel API

## Available Methods

-   get: **`api/products`**
-   post: **`api/products`**
-   post: **`api/products/id`**
-   put: **`api/products`**

## Workflow

-   Register using **`api/register`**

    -   inside body put **`name, email, password, password_confirmation`**
    -   on headers select **`Key as Accept`** with **`value as application/json`**
    -   You will get token on response, use the token to post, update and delete data

-   To login simply put your credentials as

```
{
  "email": "test@email.com",
  "password": "password"
}
```

-   You will get the token on response use it to post put and delete data

## Post, Update & Delete data

-   After register or login save the token on request and pass the token as **Bearer Token**, Each and every time.

### To Post

-   **post request**

```
# Add the token inside the authentication which
# you will get at the time of register or login
api/products/
{
    "name": "Sample name",
    "slug": "sample-slug",
    "description": "Sample description",
    "price": 12345
}
```

### To Update

-   **put request**

```
# Add the token inside the authentication which
# you will get at the time of register or login
api/products/id
{
    "name": "Sample name",
    "slug": "sample-slug",
    "description": "Updated Sample description",
}
```

### To delete

-   **delete request**

```
api/products/id
```

-   Just send request specifying the product id with the token

### Log out and delete token

-   **post request**
-   To log out we just need to pass the bearer token, the token is enough to identify the user

```
api/logout
```
### Full API list 
```
+--------+----------+----------------------------+------+------------------------------------------------------------+------------------------------------------+
| Domain | Method   | URI                        | Name | Action                                                     | Middleware                               |
+--------+----------+----------------------------+------+------------------------------------------------------------+------------------------------------------+
|        | GET|HEAD | /                          |      | Closure                                                    | web                                      |
|        | POST     | api/login                  |      | App\Http\Controllers\AuthController@login                  | api                                      |
|        | POST     | api/logout                 |      | App\Http\Controllers\AuthController@logout                 | api                                      |
|        |          |                            |      |                                                            | App\Http\Middleware\Authenticate:sanctum |
|        | GET|HEAD | api/products               |      | App\Http\Controllers\ProductController@index               | api                                      |
|        | POST     | api/products               |      | App\Http\Controllers\ProductController@store               | api                                      |
|        |          |                            |      |                                                            | App\Http\Middleware\Authenticate:sanctum |
|        | GET|HEAD | api/products/search/{name} |      | App\Http\Controllers\ProductController@search              | api                                      |
|        | GET|HEAD | api/products/{id}          |      | App\Http\Controllers\ProductController@show                | api                                      |
|        | PUT      | api/products/{id}          |      | App\Http\Controllers\ProductController@update              | api                                      |
|        |          |                            |      |                                                            | App\Http\Middleware\Authenticate:sanctum |
|        | DELETE   | api/products/{id}          |      | App\Http\Controllers\ProductController@destroy             | api                                      |
|        |          |                            |      |                                                            | App\Http\Middleware\Authenticate:sanctum |
|        | POST     | api/register               |      | App\Http\Controllers\AuthController@register               | api                                      |
|        | GET|HEAD | api/user                   |      | Closure                                                    | api                                      |
|        |          |                            |      |                                                            | App\Http\Middleware\Authenticate:api     |
|        | GET|HEAD | sanctum/csrf-cookie        |      | Laravel\Sanctum\Http\Controllers\CsrfCookieController@show | web                                      |
+--------+----------+----------------------------+------+------------------------------------------------------------+------------------------------------------+
```