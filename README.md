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
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzs1UiJ9.eyJleHAiOjE1OTMxMTQ5OTgsInN1YiI6MTR0MTY5fQ.9ewoBuPRRvdNMkJ_DFSQtLofnx11ezEoD3kTt2-MI7Q",
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
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzs1UiJ9.eyJleHAiOjE1OTMxMTQ5OTgsInN1YiI6MTR0MTY5fQ.9ewoBuPRRvdNMkJ_DFSQtLofnx11ezEoD3kTt2-MI7Q",
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
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzs1UiJ9.eyJleHAiOjE1OTMxMTQ5OTgsInN1YiI6MTR0MTY5fQ.9ewoBuPRRvdNMkJ_DFSQtLofnx11ezEoD3kTt2-MI7Q&context%5Btype%5D=School&context%5Bid%5D=1' 'https://auth.kicksite.net/v1/users/sessions'```

Ruby:
https://github.com/KicksiteDev/kicksite_auth_client
```
UserSession.new(
  token: '<auth_token>'
).validate!
```
