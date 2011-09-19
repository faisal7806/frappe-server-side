# Automatic Update System

The product needs to be updated regularly - The types of updates are:

1. DocType updates (reload_doc)
2. Data scrubbing / schema updates (sql queries)

These updates can be published and subscribed via a web-service. All subscribed databases should regularly poll for new updates.

## API

All updates should be saved on a db at erpnext.com and it should expose publish and subscribe mechanisms (the publishing should be done only when a secret key is passed)

### Publish

Publish updates via:

    updates.py publish "command"

Connect URL:

    erpnext.com/updates.cgi?type=publish&key=secret&update=[code]

Returns:

    {"update_number":"xxx"}, 

### Subscribe

To subscribe:

    erpnext.com/update.cgi?type=subscribe&user_id=%s

Returns:

    {"user_key":[hash]}

### Get

To get the latest updates, the client must subscribe to the 

    erpnext.com/updates.cgi?type=get_update&version=xxx&user_key=[client_hash]

Returns:

    {"new_version":"yyy", "updates":["update1", "update2"]}

## Implementation

#### Update Server

- Update Manager to keep a db of all updates
- users
- accept "publish", "subscribe" and "get_updates" (via cgi?)

#### Client

- subscribe to update manager
- via a scheduled event, poll for updates and execute them



