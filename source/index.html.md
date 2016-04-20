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
  A JSON object containing a message that says a user's email has been validated
```
Sets a user's `validated` property to `true`.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email address |
| key | the validation string sent to the user via email |

## Route:  `/send-reset-email`

#### Verb: `POST`
```shell
Example return value: for #POST
{
  "success": "true",
  "message": "Sent password reset email."
}
Description:
  A JSON object stating a reset email has been sent successfully.
```
Sends an email with a password reset link to the provided address.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email address |


## Route:  `/reset-password`

#### Verb: `POST`
```shell
Example return value: for #POST
{
  "success": "true",
  "message": "Updated password for molecularplayground@gmail.com."
}
Description:
  A JSON object stating a password has been successfully reset.
```
Given a user's email, resets their password to the given value assuming the key we've saved matched the key given.

|   Parameter   |  Description  |
|---------------|---------------|
| key | the key sent to the user in the reset email |
| email | the user's email address |
| password | the user's password |


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
  {
    "success":true,
    "message": [
      {
        "mid":1
        "name":"4CS1",
        "link":"http://104.236.54.250:8000/api/molecule/files/159ba9f22a319144d9fac8ec7843136f"
      }
    ]
  }

Description:
  An array of JSON molecule objects containing the name and link properties.
```

Returns all molecule details contained in the database.

## Route:  `/<name>`

#### Verb: `GET`

```shell
Example return value for #GET:
  {
    "success":true,
    "message": [
      {
        "mid":1
        "name":"4CS1",
        "link":"http://104.236.54.250:8000/api/molecule/files/159ba9f22a319144d9fac8ec7843136f"
      }
    ]
  }

Description:
  An array of JSON molecule objects whose name is "like" the one passed to this route.
```

Returns all molecule details contained in the database whose name is "like" the one passed to this route.

## Route:  `/upload`

#### Verb: `POST`

```shell
Example return value for #POST:
  {
    "success":true,
    "message": {
      "success": true,
      "message": "d7fb73cb4edd1bec576701ab1aab3715"
    }
  }

Description:
  The name of the molecule object as it is saved in the microservice.
```

Returns the name of the molecule object as it is saved in the microservice. This name is used to construct the file's URL.

|   Parameter   |  Description  |
|---------------|---------------|
| molecule | the molecule file being uploaded |
| name | the new name of the molecule |
| type | ??? (String) |

## Route:  `/files/<filename>`

#### Verb: `GET`

```shell
Example return value for #GET:
  HEADER    RNA                                     03-MAR-14   4CS1              
  TITLE     CRYSTAL STRUCTURE OF A SIMPLE DUPLEX KINK TURN, HMKT-7 WITH           
  TITLE    2 2 MG BOUND.                                                          
  COMPND    MOL_ID: 1;                                                            
  COMPND   2 MOLECULE: 5'-(*GP*GP*CP*GP*AP*AP*GP*AP*AP*CP*CP*GP*GP*GP             
  COMPND   3  *GP*AP*GP*CP*CP)-3';                                                
  COMPND   4 CHAIN: A                                                             
  SOURCE    MOL_ID: 1;                                                            
  SOURCE   2 SYNTHETIC: YES;                                                      
  SOURCE   3 ORGANISM_SCIENTIFIC: HALOARCULA MARISMORTUI;                         
  SOURCE   4 ORGANISM_TAXID: 2238                                                 
  KEYWDS    RNA, KINK TURN, METAL ION                                             
  ...

Description:
  The molecule file with the header Content-Type: text/plain.
```

Returns the molecule file with the header Content-Type: text/plain.
