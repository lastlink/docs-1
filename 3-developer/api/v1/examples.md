# Examples

## GET  privileges/:groupId/
*Returns JSON object of the privileges for a given group*

#### Example Request
**GET** http://directus.dev/api/1/privileges/0

```
[
  {
    "id": "23",
    "table_name": "countries",
    "permissions": "add,edit,bigedit,delete,bigdelete,alter,view,bigview",
    "group_id": "0",
    "read_field_blacklist": null,
    "write_field_blacklist": null,
    "unlisted": null
  },
  {
    "id": "1",
    "table_name": "directus_activity",
    "permissions": "add,edit,bigedit,delete,bigdelete,alter,view,bigview",
    "group_id": "0",
    "read_field_blacklist": null,
    "write_field_blacklist": null,
    "unlisted": null
  },
  {
    "id": "18",
    "table_name": "directus_bookmarks",
    "permissions": "add,edit,bigedit,delete,bigdelete,alter,view,bigview",
    "group_id": "0",
    "read_field_blacklist": null,
    "write_field_blacklist": null,
    "unlisted": null
  }
]
```


## GET  tables/:table/rows/
*Returns a collection of table entries the authenticated user has permission to view*

Parameter  |  Example  |  Description
:-----------|:-----------|:-----------------------
**`ids`**  |  `1,2,3,5,6,7,8`  |  Comma delimited list of ids to return

#### Example Request
**GET** http://directus.dev/api/1/tables/directus_users/rows

```
{
  "active": 1,
  "inactive": 0,
  "trash": 0,
  "total": 1,
  "rows": [
    {
      "id": 3,
      "active": 1,
      "first_name": "John",
      "last_name": "Smith",
      "email": "john.smith@example.com",
      "password": "asfafspojd92en1oi2n31b412ubb1n",
      "salt": "5329e597d9afa",
      "position": "",
      "email_messages": 1,
      "last_login": null,
      "last_access": null,
      "last_page": "",
      "ip": "",
      "group": {
        	"id": 0,
        	"name": "Administrator",
        	"description": null,
        	"restrict_to_ip_whitelist": 0
      },
      "avatar": null,
      "location": "",
      "phone": "",
      "address": "",
      "city": "",
      "state": "",
      "zip": ""
    }
]
```
