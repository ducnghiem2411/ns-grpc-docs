## API

```protobuf

syntax = "proto3";

service Brick Service {
    rpc Call (Request) returns (Response) {}
}

message Request {
    string method = 1;
    string params = 2;
}

message Response {
    string result = 1;
}
```

***

## user endpoints

 - [user_notify](https://github.com/brickglobal/docs/blob/master/notify-service.md#user_notify)
 - [user_send_phone_verify](https://github.com/brickglobal/docs/blob/master/notify-service.md#user_send_phone_verify)
 - [user_send_email_verify](https://github.com/brickglobal/docs/blob/master/notify-service.md#user_send_email_verify)
 - [user_send_email_forgot_password](https://github.com/brickglobal/docs/blob/master/notify-service.md#user_send_email_forgot_password)
 - [user_subscribe_topic]()
 - [user_unsubscribe_topic]()

## server endpoints
 - [server_email_admin](https://github.com/brickglobal/docs/blob/master/notify-service.md#server_email_admin)
 - [server_publish_topic]()
 -
***

### user_notify

Send notify to a mobile user (hard & cloud wallet).


##### Parameters

`stringified object`:

    type: string <"push" | "email" | "sms">
    event: string <"hw_sent" | ... >
    to: string <"ExponentPushToken[xxx]" | "people@mail.com" | "09876542321">
    data: object (reference templates)
    

##### Returns

`string`
  
##### Example

```js
// Request
{
    method: "user_notify",
    params: JSON.stringify({
        type: "push"
        to: "test",
        password: "Test123"
    })
}

// Result
{
  result: "success"
}

```

***

### user_send_phone_verify

Sending otp code to verify phone number 


##### Parameters

`stringified object`:

    phone: string 
    otp: string
    

##### Returns

`string`
  
##### Example
```js
// Request
{
    method: "user_send_phone_verify",
    params: JSON.stringify({
        phone: "0987654321",
        otp: "1234"
    })
}

// Result
{
  result: "success"
}

```

***

### user_send_email_verify

Sending email to verify email address 


##### Parameters

`stringified object`:

    email: string 
    username: string
    url: string
    

##### Returns

`string`
  
##### Example
```js
// Request
{
    method: "user_send_email_verify",
    params: JSON.stringify({
        email: "test@mail.com",
        username: "test",
        url: "https://brick.global?email_verify=890u20asdnjlasd90...."
    })
}

// Result
{
  result: "success"
}

```

***

### user_send_email_forgot_password

Sending email to recover password


##### Parameters

`stringified object`:

    email: string 
    url: string
    

##### Returns

`string`
  
##### Example
```js
// Request
{
    method: "user_send_email_forgot_password",
    params: JSON.stringify({
        email: "test@mail.com",
        url: "https://brick.global?forgot_password=890u20asdnjlasd90...."
    })
}

// Result
{
  result: "success"
}

```

***

### user_subscribe_topic

Register subscribe to a topic for client (web & mobile)

##### Parameters

`stringified object`:

    registrationToken: string
    topicName: string

##### Returns

`string`

##### Example

```js
// Request
{
    method: "user_subscribe_topic",
    params: JSON.stringify({
        registrationToken: "regis-token-get-from-fcm-client"
        topicName: "/topics/name-of-the-topic"
    })
}

// Result
{
  result: "subscribe success"
}

```

***

### user_unsubscribe_topic

Unsubscribe to a topic for client (web & mobile)

##### Parameters

`stringified object`:

    registrationToken: string
    topicName: string

##### Returns

`string`

##### Example

```js
// Request
{
    method: "user_unsubscribe_topic",
    params: JSON.stringify({
        registrationToken: "regis-token-get-from-fcm-client"
        topicName: "/topics/name-of-the-topic"
    })
}

// Result
{
  result: "unsubscribe success"
}

```

***

### server_email_admin

Sending email for admin 


##### Parameters

`stringified object`:

    email: string 
    subject: string
    body: string <in html>
    text: string
    

##### Returns

`string`
  
##### Example

```js
// Request
{
    method: "server_email_admin",
    params: JSON.stringify({
        email: "admin07@gmail.com"
        subject: "BRICK ADMIN: RESET PASSWORD",
        body: "some text",
        text: "some text"
    })
}

// Result
{
  result: "success"
}

```

***

### server_publish_topic

Send all notification for user who subscribe to the topic


##### Parameters

`stringified object`:

    "topicName": "/topics/fucking-topic",
    "topicPayload": {
        "data": {
                "dataThichVietGiThiViet": "nhu the nay",
                "khongCoKeyMessage_type": "la duoc",
                "khongCoKeyFrom" : "la duoc"
        },
        "notification": {
                "title": "this is stupid tilte",
                "body": "stupid body"
            }
        },
        "options"?: {

        }

##### Returns

`string`
  
##### Example

```js
// Request
{
    method: "server_email_admin",
    params: JSON.stringify({
        "topicName": "/topics/fucking-topic",
        "topicPayload": {
            "data": {
                "dataThichVietGiThiViet": "nhu the nay",
                "khongCoKeyMessage_type": "la duoc",
                "khongCoKeyFrom" : "la duoc"
            },
            "notification": {
                "title": "this is stupid tilte",
                "body": "stupid body"
            }
        }
    })
}

// Result
{
  result: "send topic success"
}

```