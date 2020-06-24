# API-Documentation

## Authentication
https://auth.kicksite.net/

### Create new user session
`POST  https://auth.kicksite.net/v1/users/new/sessions`
```
{
  "login": "<username>",
  "password": "<password>",
  "context": {
    "type": "School",
    "id": 1
  }
}
```
Response Example:
```
 {
  "token": "<auth_token>",
  "user": {
    "id": 1,
    "username": "<username>",
    "email": "",
    "created_at": null,
    "updated_at": "2020-04-29T16:15:51.821Z",
    "show_system_announcement": true,
    "vault_id": null,
    "unread_count": 0,
    "secondary_email": null,
    "person_id": 1,
    "role": null,
    "confirm_terms_of_use": true,
    "disabled": false,
    "last_request_at": null,
    "context_type": null,
    "context_id": null,
    "person_type": "Administrator",
    "permissions": [
      "memberships",
      "maps",
      "messages",
      "payments",
      "groups",
      "reports",
      "attendances",
      "employees",
      "announcements",
      "documents",
      "events",
      "video",
      "inventory",
      "invoices",
      "invitations",
      "recent_activity",
      "billing",
      "vitals"
    ]
  }
}
```

Curl:
```
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'login=<username>&password=<password>&context%5Btype%5D=School&context%5Bid%5D=1' 'https://auth.kicksite.net/v1/users/new/sessions'
```

Ruby:
https://github.com/KicksiteDev/kicksite_auth_client
```
UserSession.new(
  email: '<username>',
  password: '<password>',
  context: {
    type: 'School',
    id: 1
  }
).authenticate!
```

### Validate existing user session
`POST  https://auth.kicksite.net/v1/users/sessions`
```
{
  "token": "<auth_token>",
  "context": {
    "type": "School",
    "id": 1
  }
}
```
Response Example:
```
 {
  "token": "<auth_token>",
  "user": {
    "id": 1,
    "username": "<username>",
    "email": "",
    "created_at": null,
    "updated_at": "2020-04-29T16:15:51.821Z",
    "show_system_announcement": true,
    "vault_id": null,
    "unread_count": 0,
    "secondary_email": null,
    "person_id": 1,
    "role": null,
    "confirm_terms_of_use": true,
    "disabled": false,
    "last_request_at": null,
    "context_type": null,
    "context_id": null,
    "person_type": "Administrator",
    "permissions": [
      "memberships",
      "maps",
      "messages",
      "payments",
      "groups",
      "reports",
      "attendances",
      "employees",
      "announcements",
      "documents",
      "events",
      "video",
      "inventory",
      "invoices",
      "invitations",
      "recent_activity",
      "billing",
      "vitals"
    ]
  }
}
```

Curl:
```
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'token=<auth_token>&context%5Btype%5D=School&context%5Bid%5D=1' 'https://auth.kicksite.net/v1/users/sessions'
```

Ruby:
https://github.com/KicksiteDev/kicksite_auth_client
```
UserSession.new(
  token: '<auth_token>'
).validate!
```

## Data Retrieval/Modification
https://api.kicksite.net/

### Get Lead Capture Form Information
`GET  https://api.kicksite.net/v1/schools/1/bizbuilder/forms/<access_token>`

Response Example: [200]
```
{
  "name": "New form (June 23, 2020 11:15AM)",
  "status": "active",
  "create_prospect": true,
  "fields": [
    {
      "key": "phone",
      "label": "Phone Number",
      "type": "tel",
      "order": 3,
      "required": true,
      "created_at": "2020-06-23T16:16:09.826Z",
      "updated_at": "2020-06-23T16:16:09.826Z"
    },
    {
      "key": "email",
      "label": "Email",
      "type": "email",
      "order": 2,
      "required": true,
      "created_at": "2020-06-23T16:16:09.822Z",
      "updated_at": "2020-06-23T16:16:09.822Z"
    },
    {
      "key": "name",
      "label": "Name",
      "type": "text",
      "order": 1,
      "required": true,
      "created_at": "2020-06-23T16:16:09.816Z",
      "updated_at": "2020-06-23T16:16:09.816Z"
    }
  ],
  "id": 2166,
  "access_token": "<access_token>",
  "submissions_count": 0,
  "created_at": "2020-06-23T16:15:30.520Z",
  "updated_at": "2020-06-23T16:15:30.520Z",
  "theme": {
    "primary_color": "#f2a900",
    "secondary_color": "#404040",
    "tertiary_color": "#f2f2f2"
  }
}
```

Curl:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <access_token>' 'https://api.kicksite.net/v1/schools/1/bizbuilder/forms/<access_token>'
```

Ruby:
https://github.com/KicksiteDev/kicksite_svc_client
```
KicksiteSvcBearerAuth.connection.bearer_token = '<access_token>'

Kicksite::Schools::Bizbuilder::Form.find('<access_token>', params: { school_id: 1 })
```

#### Submit Lead Capture Form Information
`POST  http://api.kicksite.net/v1/schools/1/bizbuilder/forms/<access_token>/submissions`
```
{
  "payload": {
     "phone": "1234567890",
     "email": "prospect@email.com",
     "name": "Firstname Lastname"
  }
}
```
Response Example: [201]
```
{
  "payload": {
    "phone": "1234567890",
    "email": "prospect@email.com",
    "name": "Firstname Lastname"
  },
  "lead_capture_form_id": 2166,
  "created_at": "2020-06-24T20:25:42.810Z",
  "prospect_id": 1
}
```

Curl:
```
curl --location --request POST 'http://api.kicksite.net/v1/schools/119/bizbuilder/forms/<access_token>/submissions' \
--header 'Authorization: Bearer <access_token>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "payload": {
        "phone": "1234567890",
        "email": "prospect@email.com",
        "name": "Firstname Lastname"
    }
}'
```

Ruby:
https://github.com/KicksiteDev/kicksite_svc_client
```
KicksiteSvcBearerAuth.connection.bearer_token = '<access_token>'

form = Kicksite::Schools::Bizbuilder::Form.find('<access_token>', params: { school_id: 1 })
form.id = form.access_token
form.submit({
  phone: "1234567890",
  email: "prospect@email.com",
  name: "Firstname Lastname"
})
```
