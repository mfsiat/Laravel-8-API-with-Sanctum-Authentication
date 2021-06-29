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
