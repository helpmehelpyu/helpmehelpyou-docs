# API Documentation

## Media

### GET Media by ID

Fetch an image/video/media by it's `mediaId`.

```
GET /media/{mediaId}
```

#### <span style='font-size: 1.2em'> Request </span>

**Path Parameters**

| Name    | Type     | Description                     |
| ------- | -------- | ------------------------------- |
| mediaId | `String` | The ID of the image/video/media |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green; font-weight: bold'> 200 </span>**

Media was successfuly found and returned.
Returns a `application/json` Media object with some fields truncated.

```json
{
	mediaID: String,
	author: {
		id: String,
		firstName: String,
		lastName: string,
	},
	source: String,
	title: String,
	description: String,
	uploadedDate: Date,
}
```

| Name             | Type     | Description                                         |
| ---------------- | -------- | --------------------------------------------------- |
| mediaId          | `String` | The ID of the image/video/media                     |
| author           | `User`   | The author of the media                             |
| author.id        | `String` | The ID of the author of the media                   |
| author.firstName | `String` | The first name of the author of the media           |
| author.lastName  | `String` | The last name of the author of the media            |
| source           | `String` | The URL of where the source of the media is located |
| title            | `String` | The title of the media                              |
| description      | `String` | The description of the media                        |
| uploadDate       | `Date`   | The date when the media was uploaded                |

#### **<span style='color: red; font-weight: bold'> 404 </span>**

Media with the given `mediaId` was not found.

```json
{
	type: String
	message: String
}
```

| Name    | Type     | Description                    |
| ------- | -------- | ------------------------------ |
| type    | `String` | The type of Error that occured |
| message | `String` | The Error message              |

<!-- tabs:end -->

### UPLOAD new Media

Upload a new image or video.

```
POST /media
```

#### <span style='font-size: 1.2em'> Request </span>

**Authorization: Bearer**

Content-Type: `multipart/form-data`

Make sure that in the Request Body you have the lines

```
Content-Disposition: form-data; name="title"

Content-Disposition: form-date; name="media"; filename="filename.ext"
```

That is, the title and file are required fields.

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green; font-weight: bold'> 201 </span>**

Media was successfully uploaded and saved.

```json
{
	mediaId: String
}
```

| Name    | Type     | Description                        |
| ------- | -------- | ---------------------------------- |
| mediaId | `String` | The ID of the newly uploaded media |

#### **<span style='color: red; font-weight: bold'> 400 </span>**

Unsupported file format or data.

```json
{
	fileError: {
		type: string,
		message: string,
	}
	errors: [
		{
			type: string,
			message: string,
		}
	]
}
```

<!-- tabs:end -->

### EDIT existing Media

Edit the existing Media corresponding to `mediaId`

```
PATCH /media/{mediaId}
```

#### <span style='font-size: 1.2em'> Request </span>

**Authorization: Bearer**

**Path Parameters**

| Name    | Type     | Description         |
| ------- | -------- | ------------------- |
| mediaId | `String` | The ID of the media |

#### <span style='font-size: 1.2em'> Request Body</span>

Both fields are optional.

```json
{
	title: String,
	description: String,
}
```

| Name        | Type     | Description                      |
| ----------- | -------- | -------------------------------- |
| title       | `String` | The new title of the media       |
| description | `String` | The new description of the media |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

Media was successfully updated.

#### **<span style='color: red;font-weight: bold'> 404 </span>**

Media with this `mediaID` could not be found.

```json
{
	type: String
	message: String
}
```

| Name    | Type     | Description                    |
| ------- | -------- | ------------------------------ |
| type    | `String` | The type of Error that occured |
| message | `String` | The Error message              |

#### **<span style='color: red;font-weight: bold'> 400 </span>**

Invliad title or description

```json
{
	type: String
	message: String
}
```

| Name    | Type     | Description                    |
| ------- | -------- | ------------------------------ |
| type    | `String` | The type of Error that occured |
| message | `String` | The Error message              |

<!-- tabs:end -->

### DELETE existing Media

Delete the media with the corresponding `mediaId`

```
DELETE /media/{mediaId}
```

#### <span style='font-size: 1.2em'> Request </span>

**Authorization: Bearer**

**Path Parameters**

| Name    | Type     | Description                     |
| ------- | -------- | ------------------------------- |
| mediaId | `String` | The ID of the image/video/media |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

Media with the corresponding `mediaId` was successfully deleted.

#### **<span style='color: red;font-weight: bold'> 404 </span>**

Media with this `mediaID` could not be found.

```json
{
	type: String
	message: String
}
```

| Name    | Type     | Description                    |
| ------- | -------- | ------------------------------ |
| type    | `String` | The type of Error that occured |
| message | `String` | The Error message              |

<!-- tabs:end -->

## User

### Register a New User

Register a new User with the given data.

```
POST /users/signup
```

#### <span style='font-size: 1.2em'> Request </span>

**Request Body**

| Name        | Type     | Description                   | Required                    |
| ----------- | -------- | ----------------------------- | --------------------------- |
| firstName   | `String` | The first name of the User    | Yes                         |
| lastName    | `String` | The last name of the User     | Yes                         |
| email       | `String` | The email address of the User | Yes                         |
| password    | `String` | The User's password           | Yes                         |
| phoneNumber | `String` | The phone number of the User  | No (empty string when null) |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 201 </span>**

A new User with the specified data has successfully been created.

```json
{
	userId: String (is uuid)
}
```

#### **<span style='color: red;font-weight: bold'> 400 </span>**

A new User could not be created with the given data. Invalid data entered.

```json
{
	errors: [
		{
			type: String,
			message: String,
			value?: String,
			location?: String,
		}
	]
}
```

<!-- tabs:end -->

### Login an Existing User

Log in a User with their email and password.

#### <span style='font-size: 1.2em'> Request </span>

#### Request Body

| Name     | Type     | Description                   | Required |
| -------- | -------- | ----------------------------- | -------- |
| email    | `String` | The email address of the User | Yes      |
| password | `String` | The User's password           | Yes      |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 201 </span>**

On successful login, return the authentication token for the user.

```json
{
	authToken: String
}
```

#### **<span style='color: red;font-weight: bold'> 403 </span>**

Incorrect email or password entered.

```json
{
    "type": "InvalidLoginInformationError",
    "message": "Invalid email or password"
}
```

<!-- tabs:end -->

### Update an Existing User

Edit the details of an existing user

```
POST /users/:userId
```

#### <span style='font-size: 1.2em'> Request </span>

**Authorization: Bearer**

**Path Parameters**

| Name   | Type     | Description                     |
| ------ | -------- | ------------------------------- |
| userId | `String` | The id of the user to be edited |

#### Request Body

| Name        | Type     | Description                   | Required |
| ----------- | -------- | ----------------------------- | -------- |
| firstName   | `String` | The first name of the User    | No       |
| lastName    | `String` | The last name of the User     | No       |
| email       | `String` | The email address of the User | No       |
| phoneNumber | `String` | The phone number of the User  | No       |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

User is successfully updated

Returns the updated user object on success.

```json
{
	id: String,
	firstName: String,
	lastName: String,
	email: String,
	password: String,
	phoneNumber: String
}
```

| Name        | Type     | Description                                                                    | Required                    |
| ----------- | -------- | ------------------------------------------------------------------------------ | --------------------------- |
| id          | `String` | The ID (autogenerated uuid) of the User which can be used to query the db with | Yes                         |
| firstName   | `String` | The first name of the User                                                     | Yes                         |
| lastName    | `String` | The last name of the User                                                      | Yes                         |
| email       | `String` | The email address of the User                                                  | Yes                         |
| password    | `String` | The User's password                                                            | Yes                         |
| phoneNumber | `String` | The phone number of the User                                                   | No (empty string when null) |

#### **<span style='color: red;font-weight: bold'> 400 </span>**

Invalid user input.

```json
{
	errors: [
		{
			type: String,
			message: String,
			value?: String,
			location?: String,
		}
	]
}
```

| Name     | Type     | Description                               | Required |
| -------- | -------- | ----------------------------------------- | -------- |
| type     | `String` | The name of the error                     | Yes      |
| lastName | `String` | The error message                         | Yes      |
| value    | `String` | The invalid input value                   | No       |
| location | `String` | The location where the value was inputted | No       |

<!-- tabs:end -->

### Delete a User

Delete an existing user.

#### <span style='font-size: 1.2em'> Request </span>

**Authorization: Bearer**

**Path Parameters**

| Name   | Type     | Description                      |
| ------ | -------- | -------------------------------- |
| userId | `String` | The id of the user to be deleted |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

User was successfully deleted.

```
OK
```

#### **<span style='color: red;font-weight: bold'> 500 </span>**

User could not be deleted.

```json
{
    "message": "Unable to delete the requested resource"
}
```

| Name    | Type     | Description       |
| ------- | -------- | ----------------- |
| message | `String` | The error message |

<!-- tabs:end -->

## Links

### Create a New Link

Create a new Link with the given name and url

```
POST /links
```

#### <span style='font-size: 1.2em'> Request </span>

**Authentication Bearer**

**Request Body**

| Name | Type     | Description          |
| ---- | -------- | -------------------- |
| name | `String` | The name of the link |
| url  | `String` | The url of the link  |

All fields are required

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 201 </span>**

Link was successfully created

```json
{
	id: number,
	owner: {
		id: String,
		firstName: String,
		lastName: String,
	}
	name: String,
	url: String
}
```

| Name            | Type     | Description                            |
| --------------- | -------- | -------------------------------------- |
| id              | `String` | The id of the link                     |
| owner           | `String` | The owner of the link                  |
| owner.id        | `String` | The id of the owner of the link        |
| owner.firstName | `String` | The firstName of the owner of the link |
| owner.lastName  | `String` | The lastName of the owner of the link  |
| name            | `String` | The name of the link                   |
| url             | `String` | The url of the link                    |

#### **<span style='color: red;font-weight: bold'> 400 </span>**

Invalid User input.

```json
{
	errors: [
		{
			type: String,
			msg: String,
			value: String,
			location: String,
		}
	]
}
```

| Name     | Type     | Description                               |
| -------- | -------- | ----------------------------------------- |
| type     | `String` | The name of the error                     |
| lastName | `String` | The error message                         |
| value    | `String` | The invalid input value                   |
| location | `String` | The location where the value was inputted |

<!-- tabs:end -->

### Update an Exist Link

Update an existing Link with the associated LinkId

```
PUT /links/:linkId
```

#### <span style='font-size: 1.2em'> Request </span>

**Authentication Bearer**

**Path Parameters**

| Name   | Type     | Description        |
| ------ | -------- | ------------------ |
| linkId | `String` | The id of the Link |

#### Request Body

| Name | Type     | Description              |
| ---- | -------- | ------------------------ |
| name | `String` | The new name of the Link |
| url  | `String` | The new url of the Link  |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

The Link was successfully updated

```json
{
	id: number,
	owner: {
		id: String,
		firstName: String,
		lastName: String,
	}
	name: String,
	url: String
}
```

| Name            | Type     | Description                            |
| --------------- | -------- | -------------------------------------- |
| id              | `String` | The id of the link                     |
| owner           | `String` | The owner of the link                  |
| owner.id        | `String` | The id of the owner of the link        |
| owner.firstName | `String` | The firstName of the owner of the link |
| owner.lastName  | `String` | The lastName of the owner of the link  |
| name            | `String` | The name of the link                   |
| url             | `String` | The url of the link                    |

#### **<span style='color: red;font-weight: bold'> 400 </span>**

Invalid User input.

```json
{
	errors: [
		{
			type: String,
			msg: String,
			value: String,
			location: String,
		}
	]
}
```

| Name     | Type     | Description                               |
| -------- | -------- | ----------------------------------------- |
| type     | `String` | The name of the error                     |
| lastName | `String` | The error message                         |
| value    | `String` | The invalid input value                   |
| location | `String` | The location where the value was inputted |

<!-- tabs:end -->

### Delete Existing Link

```
DELETE /links/:linkId
```

#### <span style='font-size: 1.2em'> Request </span>

**Authentication Bearer**

**Path Parameters**

| Name   | Type     | Description        |
| ------ | -------- | ------------------ |
| linkId | `String` | The id of the Link |

#### <span style='font-size: 1.2em'> Response </span>

<!-- tabs:start -->

#### **<span style='color: green;font-weight: bold'> 200 </span>**

Link was successfully deleted.

```
OK
```

#### **<span style='color: red;font-weight: bold'> 500 </span>**

Link could not be deleted

```json
{
    "message": "unabled to delete the requested resource"
}
```

<!-- tabs:end -->
