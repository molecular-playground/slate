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


```shell
Example return value for #GET

["aaron", "alec", "tim", "ethan"],

Description:
"An array of strings combining to form every username in the database."
```


Get an array of all usernames (NOT full user objects).

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |


#### Verb: `PUT`

```shell
Example Return Value for #PUT

{

"email" : "moo@gmail.com",

"link" : "http://ms-email:3000/validate?email=moo@gmail.com&key=98CAD8C65ADBF2"

}

Description:

A JSON object containing the email of the newly created user and their full validation URL
```


Creates a new user.

|   Parameter   |  Description  |
|---------------|---------------|
| username | the username |
| password | the user's password |
| email | the user's email |
| location | (optional) the "stringified" location of the Molecular Playground installation |


## Route:  `/<username>`

#### Verb: `GET`
```shell
Example Return Value for #GET
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
```

Gets the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `DELETE`

```shell
Example return value for #DELETE:
  {
    success: true,
    message: "Deleted moosausage"
  }
Description:
  JSON object with success or fail and a cute string message
```

***Authentication required***

Deletes the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

## Route:  `/validate`

#### Verb: `POST`
```shell
Example return value: for #POST
{
  "success": "true",
  "message": "Validated moo@gmail.com"
}
Description:
  A JSON object containing the a message that says a user's email has been validated
```
Sets a user's `validated` property to `true`.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| key | the validation string sent to the user via email |

# ms-email

A microservice for sending emails.

Route Prefix: `/email`

## Route:  `/general`

#### Verb: `PUT`
```shell
Example return value for #PUT:
  "Message sent!"
Description:
  A confirmation string.
```
Sends an email to the specified address.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the recipient's email address |
| subject | the subject of the email |
| html | the message body, formatted as html |
| text | the message body, formatted as plaintext as a fallback |

## Route: `/validate`

#### Verb: `PUT`

```shell
Example return value for #PUT:
  "Message sent!"
Description:
  A confirmation string.
```
Sends a validation email to a newly registered user.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| link | the full URL with validation key |

# ms-schedule

A microservice for managing schedules and playlists.

Route Prefix: `/schedule`

## Route:  `/<username>`

#### Verb: `GET`

```shell
Example return value for #GET:
{
  "schedule": [
      {"pid":1,"startTime":"2:00pm"},
      {"pid":2,"startTime":"4:00pm"},
      {"pid":3,"startTime":"6:00pm"},
      {"pid":1,"startTime":"6:00pm"}
      ],
  "playlists": {
      "1": [1, 3, 3, 2],
      "2": [2, 1, 3],
      "3": [3, 2, 1]
  },
  "molecules": {
      "1": "link 1",
      "2": "link 2",
      "3": "link 3"
  }
}

Description: JSON object of schedule data for a user
```

Gets the single schedule and the playlists for said schedule for the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

## Route: `/`

#### Verb: `GET`

***Authentication required***

```shell
Example return value for #GET:
{
  "schedule": [
      {"pid":1,"startTime":"2:00pm"},
      {"pid":2,"startTime":"4:00pm"},
      {"pid":3,"startTime":"6:00pm"},
      {"pid":1,"startTime":"6:00pm"}
  ]
}

Description:
Single element json object containing an array of json objects
```

Gets the single schedule for the authenticated user and all of the user's playlists.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `POST`

***Authentication required***

```shell
Example return value for #POST
{
  success: true,
  message: 'Updated schedule for user ' + userid
}
```

Updates the single schedule for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| schedule | the JSON representation of the modified schedule |

## Route Prefix: `/playlist`

## Route:  `/`

#### Verb: `GET`

***Authentication required***

```shell
Example return value for #GET
{
  "playlists": [
      {
          "pid":1,
          "name":"awesome playlist 1",
          "playlist":[1,2,3]
      },
      {
          "pid":2,
          "name":"awesome playlist 2",
          "playlist":[4,1,5]
      },
      {
          "pid":3,
          "name":"awesome playlist 3",
          "playlist":[3,2,2]
      }
  ]
}
```

Gets all the playlists for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `POST`

***Authentication required***

```shell
Example return value for #POST
{
      success: true,
      message: 'Updated playlist ' + data.pid
  }
```

Updates a specified playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| pid | the ID of the playlist |
| playlist | the JSON representation of the modified playlist |

#### Verb: `PUT`

***Authentication required***

```shell
Example return value for #PUT
{
        success: true,
        message: "Added playlist",
        pid: playlistID
    }
```

Creates a new playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| name | the name of the new playlist |
| playlist | the JSON representation of the new playlist |

## Route:  `/rename`

#### Verb: `POST`

***Authentication required***
```shell
Example return value for #POST
{
    success: true,
    message: 'Playlist ' + data.pid + ' renamed to ' + data.name
}
```

Renames a specific playlist for the authenticated user.

|   Parameter   |  Description  |
|---------------|---------------|
| pid | the ID of the playlist |
| name | the new name of the playlist |


# ms-molecules

A microservice for retrieving the full list of Molecular Playground molecules.

Route Prefix: `/molecules`

## Route:  `/`

#### Verb: `GET`

```shell
Example return value for #GET:
  [
  {
    "name": "water",
    "link": "http://mshosting:3000/h20.pb"
  }
  ]
Description:
  An array of JSON molecule objects containing the name and link properties.
```


Returns all molecule details contained in the database.
