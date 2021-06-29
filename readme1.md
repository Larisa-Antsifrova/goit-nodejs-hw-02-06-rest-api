![Banner](./banner.png)

# REST API Contacts Project

The Web API allows to register users and handle their collections of contacts.

## Scripts

### To launch the project in development mode

```shell

npm run start:dev

```

### To launch the project in production mode

```shell

npm start

```

## Endpoints

### /api/users/signup - to register a new user

- Email and password are required. Name is optional.
- If no name is provided, 'Awesome Guest' is set as default.
- Fields are validated.
- If the email is already in use, the error of conflict is returned.
- If validation is successful and email is unique, the password is hashed and the new user is saved in database.
- No authentication token is returned since verification stage via email is implemented.

#### Registration request

```shell

POST /api/users/signup
Content-Type: application/json
RequestBody: {
  "name": "Example Examplovich",
  "email": "example@mail.com",
  "password": "example123"
}

```

### /api/users/login - to log an existing user in

- Email and password are required.
- Email and password fields are validated only for their presence.
- If a user with the provided e-mail and or password does not exist in database, general error message is returned.
- If validation is successful, credentials are right, and the user is verified the JSON Web Token is created and returned.
- JWT has limited life span.

#### Login request

```shell

POST /api/users/login
Content-Type: application/json
RequestBody: {
  "email": "example@mail.com",
  "password": "example123"
}

```

### /api/users/logout - to log a user out

- Sets JWT to null.
- Returns nothing, but No Content status.

#### Logout request

```shell

POST /api/users/logout
Authorization: "Bearer {{token}}"

```

### /api/users/current - to get a current user

#### Current user request

```shell

GET /api/users/current
Authorization: "Bearer {{token}}"

```

### /api/users - to update a current user

#### Update a user request

```shell

PATCH /api/users
Content-Type: application/json
Authorization: "Bearer {{token}}"
RequestBody: {
  "subscription": "pro"
}

```

### /api/users/avatars - to update a user's avatar

#### Update avatar request

```shell

PATCH /api/users/avatars
Content-Type: multipart/form-data
Authorization: "Bearer {{token}}"
RequestBody: <uploaded image>

```

### /api/users/verify - to resend verification e-mail

#### Resend verification email request

```shell

POST /api/users/verify
Content-Type: application/json
RequestBody: {
  "email": "example@mail.com"
}

```

### /api/users/verify/:verificationToken - to confirm account via e-mail

#### Account confirmation request

```shell

GET /api/users/verify/:verificationToken

```

---

### /api/contacts - to get the list of all current user's contacts

### Get all contacts request

```shell

GET /api/contacts
Authorization: "Bearer {{token}}"

```

### /api/contacts/:contactId - to manipulate the contact with specific id

### Get a contact by ID request

```shell

GET /api/contacts/:contactId
Content-Type: application/json
Authorization: "Bearer {{token}}"

```

### Update a contact request

```shell

PUT /api/contacts/:contactId
Content-Type: application/json
Authorization: "Bearer {{token}}"
RequestBody: {
  "email": "new-example@mail.com"
}

```

### Delete a contact request

```shell

DELETE /api/contacts/:contactId
Content-Type: application/json
Authorization: "Bearer {{token}}"

```

### /api/contacts/:contactId/favorite - to update a contact's favorite field

### Update favorite field of a contact request

```shell

PATCH /api/contacts/:contactId/favorite
Content-Type: application/json
Authorization: "Bearer {{token}}"
RequestBody: {
  "favorite": true
}

```

## Tools and resources

- JavaScript (Node.js) - as primary language.
- [Express](https://expressjs.com/) - Node.js web application framework.
- [bcryptjs](https://www.npmjs.com/package/bcryptjs) - to hash passwords.
- [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) - to generate, sign, verify JWT.
- [passport-jwt](https://www.npmjs.com/package/passport-jwt) - to implement JWT strategy authentication.
- [helmet](https://www.npmjs.com/package/helmet) - to secure the Web API.
- [express-rate-limit](https://www.npmjs.com/package/express-rate-limit) - to set rate limits on requests to the Web API.
- [express-query-boolean](https://www.npmjs.com/package/express-query-boolean) - to parse boolean values from req.query.
- [Joi](https://joi.dev/api/) - to validate data provided in POST requests.
- [gravatar](https://www.npmjs.com/package/gravatar) - to set default avatar for newly registered users.
- [jimp](https://www.npmjs.com/package/jimp) - to format an avatar image.
- [multer](https://www.npmjs.com/package/multer) - to handle avatars uploads.
- [mongoose](https://www.npmjs.com/package/mongoose) - to handle requests to Mongo DB collections.
- [mongoose-paginate-v2](https://www.npmjs.com/package/mongoose-paginate-v2) - to implement server side pagination of user's contacts.
- [mailgen](https://www.npmjs.com/package/mailgen) - to generate verification email.
- [SendGrid](https://sendgrid.com/) - to send verification emails.
- [jest](https://www.npmjs.com/package/jest) - for unit tests.

## Credits

- [Nadia](https://github.com/NadyaHristuk) - mentor & supervisor
- [Larisa](https://github.com/Larisa-Antsifrova) - developer
