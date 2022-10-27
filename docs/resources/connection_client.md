---
page_title: "Resource: auth0_connection_client"
description: |-
  With this resource, you can manage enabled clients on a connection.
  ~> Avoid using the enabledclients property on the "auth0connection" if making use of this resource, to avoid unexpected behavior.
---

# Resource: auth0_connection_client

With this resource, you can manage enabled clients on a connection.

~> Avoid using the enabled_clients property on the "auth0_connection" if making use of this resource, to avoid unexpected behavior.

## Example Usage

```terraform
resource "auth0_connection" "my_conn" {
  name     = "My-Auth0-Connection"
  strategy = "auth0"
  # Avoid using the enabled_clients = [...],
  # if using the auth0_connection_client resource.
}

resource "auth0_client" "my_client" {
  name = "My-Auth0-Client"
}

resource "auth0_connection_client" "my_conn_client_assoc" {
  connection_id = auth0_connection.my_conn.id
  client_id     = auth0_client.my_client.id
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `client_id` (String) ID of the client for which the connection is enabled.
- `connection_id` (String) ID of the connection on which to enable the client.

### Read-Only

- `id` (String) The ID of this resource.
- `name` (String) The name of the connection on which to enable the client.
- `strategy` (String) The strategy of the connection on which to enable the client.

## Import

Import is supported using the following syntax:

```shell
# This resource can be imported by specifying the
# connection ID and client ID separated by ":".
#
# Example:
terraform import auth0_connection_client.my_conn_client_assoc con_XXXXX:XXXXXXXX
```