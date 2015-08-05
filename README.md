# mint

[![Build Status](https://travis-ci.org/zalando-stups/mint-storage.svg?branch=master)](https://travis-ci.org/zalando-stups/mint-storage)

mint is the secret rotator and distributor for the STUPS ecosystem.

## Download

Releases are pushed as Docker images in the [public Docker registry](https://registry.hub.docker.com/u/stups/):

You can run mint by starting it with Docker:

    $ docker run -it stups/mint-storage

## Requirements

* PostgreSQL 9.4+

## Configuration

Configuration is provided via environment variables during start.

### Mint Storage

Variable                | Mandatory? | Default                 | Description
----------------------- | ---------- | ----------------------- | -----------
MINT_USERNAME_PREFIX    | no         |                         | Prefix for the user id of the service user. E.g. app-id: `kio` and prefix: `stups_` will result in `stups_kio`
HTTP_PORT               | yes        | `8080`                  | TCP port to provide the HTTP API.
HTTP_CORS_ORIGIN        | yes        |                         | Domain for cross-origin JavaScript requests. If set, the Access-Control headers will be set.
HTTP_TOKENINFO_URL      | no         |                         | Mandatory to enable OAuth 2.0 security! Incoming access tokens will be verified using this endpoint
HTTP_KIO_URL            | yes        |                         | URL of [Kio](https://github.com/zalando-stups/kio). Will be used to verify app ids.
HTTP_ESSENTIALS_URL     | yes        |                         | URL of [essentials](https://github.com/zalando-stups/essentials). Will be used to verify scopes.
HTTP_TEAM_SERVICE_URL   | yes        |                         | URL of the team API. Will be used to verify, that users may only edit their applications of their teams
DB_SUBNAME              | yes        | `//localhost:5432/mint` | JDBC connection information of your database.
DB_USER                 | yes        | `postgres`              | Database user.
DB_PASSWORD             | yes        | `postgres`              | Database password.

Example:

```
$ docker run -it \
    -e HTTP_CORS_ORIGIN="*" \
    -e DB_USER=mint \
    -e DB_PASSWORD=mint123 \
    stups/mint-storage
```

## Building

    $ lein do uberjar, scm-source, docker build

## Releasing

    $ lein release :minor

## Developing

Mint embeds the [reloaded](http://thinkrelevance.com/blog/2013/06/04/clojure-workflow-reloaded) workflow for interactive
development:

    $ lein repl
    user=> (go)
    user=> (reset)

## License

Copyright © 2015 Zalando SE

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
