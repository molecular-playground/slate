# Molecular Playground API

API calls are of the form:

`<verb> <host>/api/<microserivce-prefix>[<route>]`

e.g.

`GET /api/users/`

will return a `JSON` payload containing all users in the system.

# ms-users

A microservice for accessing and modifying users.

## Route Prefix: `/user`

## Route:  `/`

#### Verb: `GET`

Get all users.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `POST`

***Authentication required***

Updates a user object.

|   Parameter   |  Description  |
|---------------|---------------|
| username | the username |
| location | (optional) the "stringified" location of the Molecular Playground installation |

#### Verb: `PUT`

Creates a new user.

|   Parameter   |  Description  |
|---------------|---------------|
| username | the username |
| password | the user's password |
| email | the user's email |
| location | (optional) the "stringified" location of the Molecular Playground installation |

## Route:  `/<username>`

#### Verb: `GET`

Gets the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

#### Verb: `DELETE`

***Authentication required***

Deletes the user with username `<username>`.

|   Parameter   |  Description  |
|---------------|---------------|
| N/A | N/A |

## Route:  `/validate`

#### Verb: `POST`

Sets a user's `validated` property to `true`.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| key | the validation string sent to the user via email |

# ms-email

A microservice for sending emails.

## Route Prefix: `/email`

## Route:  `/general`

#### Verb: `PUT`

Sends an email to the specified address.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the recipient's email address |
| subject | the subject of the email |
| html | the message body, formatted as html |
| text | the message body, formatted as plaintext as a fallback |

## Route: `/validate`

#### Verb: `PUT`

Sends a validation email to a newly registered user.

|   Parameter   |  Description  |
|---------------|---------------|
| email | the user's email |
| link | the full URL with validation key |

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
