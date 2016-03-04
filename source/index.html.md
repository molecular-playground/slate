title: Molecular Playground API

language_tabs:
  - javascript

search: true

# Molecular Playground API

API calls are of the form:

`<verb> /api/<microserivce-prefix>[<route>]`

e.g.

`GET /api/users/`

will return a `JSON` payload of all users in the system.

# ms-users

A microservice for accessing and modifying users.

## Route Prefix: `/users`

### Route:  `/`

#### Verb: `GET`

Get all users

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |o

#### Verb: `POST`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|

#### Verb: `PUT`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|

#### Verb: `DELETE`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|


# ms-users

## Get All Users

HTTP Request: `GET /`



Returns all users.
Params: none.  
Returns: array of `user` objects.  

http

Each object is an index in the array.
All users in the database will be returned.

This is an unauthenticated endpoint, meaning that **anyone** will receive responses.

##### DEPRECATION WARNING

**This enpoint is being deprecated.  It will be inexistent in all subsequent
versions of this API.**  See the ms-users-auth microservice for alternatives.

### #PUT
Creates a new user.

Returns: "User has been created!"

Params (must be Body parameters in raw JSON format):

    {
      "username": "some_username",
        "password": "some_password",
        "email": "some_email",
        "location": "some_location"
    }

Location is optional. This is an unauthenticated endpoint.

### #POST
Updates a user object.

Params:

      {
        "username": "user_name",
        "location": "some_location"
      }

Both of these parameters are optional..?

This is an authenticated endpoint.

Returns "Success" OR `some_probably_nondescriptive_error`
## /:username
Where `:username` is replaced by (you guessed it!) a username that exists in the database.

### #GET

Params: none.

Returns: one user object.

This is an unauthenticated endpoint.

### #DELETE
Deletes a single user.

Params: none.

Returns: "Deleted `user_name`" OR `some_error_message`.

This is an unauthenticated endpoint.

## /validate

### #POST
Sets a user's `validated` property to `true`

Params (must be raw JSON in `request.body `):

      {
       "email": "email_addr_of_user",
       "key": "long_string_sent_in_user_validation_email"
      }

Returns "Validated `email_address`"

This is an unauthenticaed endpoint.





























































# ms-email Endpoints v0.0.0



## /validate

### #PUT
Sends an account validation email to a (new) user.

Params (must be raw JSON in request.Body):

       {
        "email": "email_of_user_to_validate",
        "link": "full_url_with_validation_key_to_validate_user"
        }

Returns: "Message sent: `mailer_success_response_msg`" OR `descriptive_error_msg`.

This is an unauthenticated endpoint.


# ms-email

`ms-email` is a microservice that allows for email sending from other molecular-playground pages.

## Route Prefix: `/email`

### Route:  `/general`

#### Verb: `PUT`

Sends an email to an address. Parameters form the body.
All endpoints are unauthenticated, but are not going to be publicly exposed from the gateway.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `email` | the recipient's email address |
| `subject` | the subject of the email |
| `html` | the message body, formatted as html |
| `text` | the message body, formatted as plaintext as a fallback|

Return:

| Type | Example |
|------|---------|
|string|success message or fail message|


#### Verb: `POST`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|

#### Verb: `PUT`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|

#### Verb: `DELETE`

Description of route + verb.

Parameters


|   Parameter   |  Description  |
|---------------|---------------|
| `<parameter>` |`<description>`|


