# LIST OF API END POINTS FOR ANDROID APP

## BASE_URL = https://nearlikes.com/v1/api

### SEND OTP FOR LOGIN

#### URL: /client/otp/get

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"phone": "+916505551234" // should contain +91,
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
  "reply": {
    "request_id": "316763707043313235343931",
    "type": "success"
  }
}
//or if already not registered
{
  "reply": {
    message: "No account with this number.",
    "type": "error"
  }
}
```

### SEND OTP FOR REGISTER

#### URL: /client/otp/get/new

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"phone": "+916505551234" // should contain +91,
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
  "reply": {
    "request_id": "316763707043313235343931",
    "type": "success"
  }
}
//or if already registered
{
  "reply": {
    "message": "An account with this number exists.",
    "type": "error"
  }
}
```

### SEND OTP FOR RESEND

#### URL: /client/otp/resend

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"phone": "+916505551234" // should contain +91,
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
	"reply": {
		"request_id": "316763707043313235343931",
		"type": "success"
	}
}
```

### SEND OTP FOR VERIFY

#### URL: /client/otp/verify

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"phone": "+916505551234" // should contain +91,
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
  "reply": {
    "message": "OTP verified success",
    "type": "success"
  }
}
//or if already not registered
{
  "reply": {
    message: "No account with this number.",
    "type": "error"
  }
}
```

### ADD A CUSTOMER

#### URL: /client/add

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
  "name": "John",
  "age": 20,
  "insta": "@samsl",
  "followers": 500,
  "location": "Delhi",
  "phone": "+916505551234", // should contain +91,
  "token": "akJGIUSA28736248"
}
```

-   ALL are required parameters

#### RESPONSE: CUSTOMER_ID -> to be stored, used for data fetching

```json
"60c7be27edde3231c06a35a2"
```

### GET A CUSTOMER by customer id

#### URL: /client/own/fetch

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60d21590a28d9531b4d4d439"
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
  "customer": {
    "associations": [
      "60d20b46e882293924daa02c" //businesses whose stories were shared
    ],
    "cashback": [], // amounts received as cashbacks
    "createdAt": 1624378603,
    "_id": "60d21590a28d9531b4d4d439",
    "name": "John Doe",
    "insta": "@johndoe",
    "followers": 500,
    "location": "Kolkata",
    "phone": "+916505551234",
    "age": 20
    "__v": 0
  }
}
```

### GET A CUSTOMER by phone number

#### URL: /client/own/fetch/phone

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"phone": "+916505551234"
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
	"customer": {
		"associations": [
			"60d20b46e882293924daa02c" //businesses whose stories were shared
		],
		"cashback": [], // amounts received as cashbacks
		"createdAt": 1624378603,
		"_id": "60d21590a28d9531b4d4d439",
		"name": "John Doe",
		"insta": "@johndoe",
		"followers": 500,
		"location": "Kolkata",
		"phone": "+916505551234",
		"__v": 0
	}
}
```

### ADD UPI ID FOR CUSTOMER

#### URL: /client/add/upi

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60c7be27edde3231c06a35a2",
	"upi": "abc@vpa"
}
```

-   ALL are required parameters. Can be used separately to update or together to create in '/client/add/pay'

#### RESPONSE: 200

### ADD EMAIL ID FOR CUSTOMER

#### URL: /client/add/email

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60c7be27edde3231c06a35a2",
	"email": "johndoe@email.com"
}
```

-   ALL are required parameters. Can be used separately to update or together to create in '/client/add/pay'

#### RESPONSE: 200

### ADD EMAIL AND UPI ID FOR CUSTOMER

#### URL: /client/add/pay

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60c7be27edde3231c06a35a2",
	"upi": "abc@vpa",
	"email": "john@email.com"
}
```

-   ALL are required parameters.

#### RESPONSE: 200

### GET MEDIA

#### URL: /client/get/media

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60c7be27edde3231c06a35a2"
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
	"media": [
		{
			"_id": "60d20b6be882293924daa02d",
			"src": "https://res.cloudinary.com/nearlikes/image/upload/v1624378232/qirshrf4afrxayzofvx4.gif", //original image url
			"pre": "https://res.cloudinary.com/nearlikes/image/upload/c_scale,h_200,w_200/v1624378232/qirshrf4afrxayzofvx4.jpg" // thumbnail url
		}
	]
}
```

### GET AVAILABLE CAMPAIGNS

#### URL: /campaign/get/campaigns

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"followers": 500, // can be number or string
	"location": "hyderabad", // can be upper or lowercase
	"age": 40
}
```

-   ALL are required parameters

#### RESPONSE:

```json
{
	"campaigns": [
		{
			"createdAt": 1625137153,
			"_id": "60dda06a62a6e65a6810ba84",
			"ownerId": "60d20b46e882293924daa02c", // is required to form association with business owner when story is shared
			"followers": 3000,
			"location": "kolkata",
			"age": 50,
			"status": "ongoing",
			"start": 1625137259,
			"end": 1627729259,
			"brand": "chaos inc",
			"text": "Sale 60%",
			"__v": 0
		}
	]
}
```

### ADD BUSINESS ASSOCIATION FOR CUSTOMER

#### URL: /client/add/association

#### STATUS: active

#### METHOD: POST

#### BODY:

```json
{
	"id": "60c7be27edde3231c06a35a2", // self id
	"data": "60d20b46e882293924daa02c" // business owner id whose story is shared
}
```

-   ALL are required parameters

#### RESPONSE: 200 // if newly added or error is returned if present in database that can be ignored

## NOTE:

> cashback api will be added

some api parameters are subject to change as
authentication will be added and client app may or may not have to pass a security
token or api key.
