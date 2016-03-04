---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Molectular Playground API

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```javascript
    noCodeHereYet```

<aside class="notice">
Hello!
</aside>

# ms-users

## /

### #GET 
Params: none.  
Returns: array of `user` objects.  

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
# /:username
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

# /validate

### #POST
Sets a user's `validated` property to `true`

Params (must be raw JSON in `request.body `): 

      {
       "email": "email_addr_of_user",
       "key": "long_string_sent_in_user_validation_email"
      }
      
Returns "Validated `email_address`"

This is an unauthenticaed endpoint.

# ms-email
# MS-EMAIL Endpoints v0.0.0

Each section in this document contains all valid HTTP verbs that can
be called.  Section headers are the route.

# /validate

### #PUT
Sends an account validation email to a (new) user.

Params (must be raw JSON in request.Body):
       
       {
        "email": "email_of_user_to_validate",
        "link": "full_url_with_validation_key_to_validate_user"
        }
        
Returns: "Message sent: `mailer_success_response_msg`" OR `descriptive_error_msg`.

This is an unauthenticated endpoint.

# /general

### #PUT
Sends an email to an address. Request params form the email.

Params (must be raw JSON in request.Body): 

        {
         "email": "to_email_address",
         "subject": "your_subject",
         "html": "html_formatted_email_body"
         "text": "plaintext_email_body_as_fallback"
        }
        
Returns: "Message sent: `mailer_success_response_msg`" OR `descriptive_error_msg`.

This is an unauthenticated endpoint.

# The End?