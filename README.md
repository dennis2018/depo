### API

#### Store a secret

**PLEASE NEVER EVER UPLOAD UNENCRYPTED SECRETS.**

This endpoint is only meant to store **already encrypted** secrets. The
encrypted secrets are stored in plain text.

```sh-session
$ curl -XPOST -s https://envshare.dev/api/v1/secret -d "already-encrypted-secret"
```

You can add optional headers to configure the ttl and number of reads.

```sh-session
$ curl -XPOST -s https://envshare.dev/api/v1/secret -d "already-encrypted-secret" -H "envshare-ttl: 3600" -H "envshare-reads: 10"
```

- Omitting the `envshare-ttl` header will set a default of 30 days. Disable the
  ttl by setting it to 0. (`envshare-ttl: 0`)
- Omitting the `envshare-reads` header will simply disable it and allow reading
  for an unlimited number of times.

This endpoint returns a JSON response with the secret id:

```json
{
  "data": {
    "id": "HdPbXgpvUvNk43oxSdK97u",
    "ttl": 86400,
    "reads": 2,
    "expiresAt": "2023-01-19T20:47:28.383Z",
    "url": "http://envshare.dev/api/v1/secret/HdPbXgpvUvNk43oxSdK97u"
  }
}
```

#### Retrieve a secret

You need an id to retrieve a secret. The id is returned when you store a secret.

```sh-session
$ curl -s https://envshare.dev/api/v1/secret/HdPbXgpvUvNk43oxSdK97u
```

```json
{
  "data": {
    "secret": "Hello",
    "remainingReads": 1
  }
}
```
