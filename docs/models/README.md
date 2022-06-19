# Models

## User

An object representing a User entity.

| Name        | Type                  | Description                                                                       | Required                    |
| ----------- | --------------------- | --------------------------------------------------------------------------------- | --------------------------- |
| \_id        | `String`              | The ID of the User which can be used to query the db with                         | Yes                         |
| firstName   | `String`              | The first name of the User                                                        | Yes                         |
| lastName    | `String`              | The last name of the User                                                         | Yes                         |
| email       | `String`              | The email address of the User                                                     | Yes                         |
| password    | `String`              | The User's password                                                               | Yes                         |
| phoneNumber | `String`              | The phone number of the User                                                      | No (empty string when null) |
| rating      | `Int`                 | The rating of the User                                                            | Yes                         |
| links       | `Map[String, String]` | Any links and connections the User wants to incude                                | Yes (can be empty)          |
| workSamples | `Array[Media]`        | An Array of Media which can be belong to the User                                 | Yes (can be empty)          |
| skills      | `Array[String]`       | An Array of Strings representing the skills of the User which can be searched for | Yes (can be empty)          |

## Media

An object representing uploaded Media.

| Name        | Type     | Description                                                                             | Required                 |
| ----------- | -------- | --------------------------------------------------------------------------------------- | ------------------------ |
| \_id        | `String` | The ID of the Media Object which can be used to query the db for the object             | Yes                      |
| mediaId     | `String` | The ID of the Media source which can be used to fetch the source/url of the image/video | Yes                      |
| author      | `User`   | The author of the media                                                                 | Yes                      |
| source      | `String` | The URL of where the source of the media is located                                     | Yes                      |
| title       | `String` | The title of the media                                                                  | Yes                      |
| description | `String` | The description of the media                                                            | No (can be empty string) |
| uploadDate  | `Date`   | The date when the media was uploaded                                                    | Yes                      |