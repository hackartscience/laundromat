laundromat
==========
Curated video streaming site that is simply the best.

The `laundromat` is hosted [here](laundromat.hackartscience.com), and uses a variety of `OAuth` providers. It is a complete rebuild of [this](https://github.com/ilebedev/laundromat) project to fix a variety of performance, usability, and security issues.

TL;DR: how do I install one of these?
-------------------------------------

1. On the deploying machine (your laptop), meet the prerequisites:
   - `ansible`
   - `git`
2. Set up a secure internet-facing machine and make it accessible via `ssh`. 
3. Create a `./secrets.yml` file. Use `secrets_example.yml` as a starting point.
4. For each OAuth provider ([Facebook](https://developers.facebook.com/), [Google](https://console.developers.google.com), [Twitter](https://apps.twitter.com/), etc.), get an app API key and secret.
5. 

`laundromat` model
------------------

TODO

### `laundromat` media files

TODO

### `laundromat` database

TODO

API
---
The web UI of laundromat

### API Security

TLS makes communication private. Server HMAC over an auth token object (which encodes information necessary to authenticate and authorize a user). 

### Authentication

- `POST /log_in` produces a `signed_auth_token` after authenticating the user via `OAuth`. TLS the token is private.

```python
signed_auth_token = {
  auth_token: {
    provider: "Oauth_provider", # OAuth provider string
    provider_id: "ABCD", # OAuth provider ID string
    roles: ["guest", "user", "moderator", "admin"], # subset of a list of roles
    expiration_time: 1234567890 # UTC time in ms since 00:00 January 1, 1970
  },
  signature: "azAZ09" # server_hmac(auth_token)
}
```

Each authenticated interaction with the `laundromat` API verifies the `HMAC` in the `signed auth token`. If the token is authentic, and has not expeired, authentication succeeds.

### Authorization

Each auhenticated interaction with the API trivially allows controller methods to authorize the user.
For example, `DELETE /user` authorizes the posting user by ensuring `"admin"` is present in the `roles` field of its `signed_auth_token`.

### REST access

TODO

Web UI
------

TODO

### Responsive framework

TODO

### Public pages

TODO

### One-page app

TODO

### Video player

TODO

### Chromecast app

TODO

`laundromat` deployment
-----------------------

### backups

TODO
