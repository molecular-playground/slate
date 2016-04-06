# Molecular Playground API

API calls are of the form:

`<verb> <host>/api/<microserivce-prefix>[<route>]`

e.g.

`GET /api/users/`

will return a `JSON` payload containing all users in the system.

# ms-users

A microservice for accessing and modifying users.

Route Prefix: `/user`

## Route:  `/`

#### Verb: `GET`


```json
  "Example return value": ["aaron", "alec", "tim", "ethan"],
  "Description":
    "An array of strings combining to form every username in the database."
```


Get an array of all usernames (NOT full user objects).

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |


#### Verb: `PUT`

Creates a new user.

|   Parameter   |  Description  |
|---------------|---------------|
| username | the username |
| password | the user's password |
| email | the user's email |
| location | (optional) the "stringified" location of the Molecular Playground installation |

    Example Return Value

      {

        "email": "moo@gmail.com",

        "link": "http://ms-email:3000/validate?email=moo@gmail.com&key=98CAD8C65ADBF2"

      }

      Description:

        A JSON object containing the email of the newly created user and their full validation URL

## Route:  `/<username>`

#### Verb: `GET`

Gets the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

    Example Return Value
      {
        "email": "moo@gmail.com",
        "username": "moosausage",
        "uid": "1",
        password: "saltedPassword",
        date-created: "20160302Z1400132",
        "validation_url": "http://ms-email:3000/validate?email=moo@gmail.com&key=98CAD8C65ADBF2",
        "validated": "false",
        location: null
        }
      Description:
      The full user object whose username matches the one given in the route

#### Verb: `DELETE`

***Authentication required***

Deletes the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

    Example return value:
      {
        success: true,
        message: "Deleted moosausage"
      }
    Description:
      JSON object with success or fail and a cute string message

## Route:  `/validate`

#### Verb: `POST`

Sets a user's `validated` property to `true`.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| key | the validation string sent to the user via email |

    Example return value:
    {
      "success": "true",
      "message": "Validated moo@gmail.com"
    }
    Description:
      A JSON object containing the a message that says a user's email has been validated


# ms-email

A microservice for sending emails.

Route Prefix: `/email`

## Route:  `/general`

#### Verb: `PUT`

Sends an email to the specified address.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the recipient's email address |
| subject | the subject of the email |
| html | the message body, formatted as html |
| text | the message body, formatted as plaintext as a fallback |

    Example return value:
      "Message sent!"
    Description:
      A confirmation string.

## Route: `/validate`

#### Verb: `PUT`

Sends a validation email to a newly registered user.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| link | the full URL with validation key |

    Example return value:
      "Message sent!"
    Description:
      A confirmation string.

# ms-schedule

A microservice for managing schedules and playlists.

## Route Prefix: `/schedule`

## Route:  `/<username>`

#### Verb: `GET`

Gets the single schedule and the playlists for said schedule for the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

## Route: `/`

#### Verb: `GET`

***Authentication required***

Gets the single schedule for the authenticated user and all of the user's playlists.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `POST`

***Authentication required***

Updates the single schedule for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| schedule | the JSON representation of the modified schedule |

## Route Prefix: `/playlist`

## Route:  `/`

#### Verb: `GET`

***Authentication required***

Gets all the playlists for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `POST`

***Authentication required***

Updates a specified playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| pid | the ID of the playlist |
| playlist | the JSON representation of the modified playlist |

## Route:  `/`

#### Verb: `PUT`

***Authentication required***

Creates a new playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| name | the name of the new playlist |
| playlist | the JSON representation of the new playlist |

## Route:  `/rename`

#### Verb: `POST`

***Authentication required***

Renames a specific playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| pid | the ID of the playlist |
| name | the new name of the playlist |


# ms-molecules

A microservice for retrieving the full list of Molecular Playground molecules.

## Route Prefix: `/molecules`

## Route:  `/`

#### Verb: `GET`

Returns all molecule details contained in the database.

|   Parameter   |  Description  |
|---------------|---------------|
| n/a | n/a |

|  Example Return Value   |  Description  |
|---------------|---------------|
| [{"name": "water", "link": "http://mshosting:3000/h20.pb"}] | An array of JSON objects containing the NAME and LINK properties. |
