# oanhnn/laravel-echo-server

Alpine based [Laravel Echo Server](https://github.com/tlaverdure/laravel-echo-server) image.

[![Build Status](https://github.com/oanhnn/docker-laravel-echo-server/workflows/CI-CD/badge.svg)](https://github.com/oanhnn/docker-laravel-echo-server/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)
[![Docker Stars](https://img.shields.io/docker/stars/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)
[![Software License](https://img.shields.io/github/license/oanhnn/docker-laravel-echo-server.svg)](https://github.com/oanhnn/docker-laravel-echo-server/blob/master/LICENSE)

## Tags

### Version tags

Git tag  | Image tag | Badges
---------|-----------|-------
`v1.0.0` | `1.0.0`   | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/1.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:1.0.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/1.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:1.0.0)
`v2.0.0` | `2.0.0`   | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/2.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.0.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/2.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.0.0)
`v2.1.0` | `2.1.0`   | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/2.1.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/2.1.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.0)
`v2.1.1` | `2.1.1`   | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/2.1.1.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.1) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/2.1.1.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.1)
`v3.0.0` | `3.0.0`   | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/3.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:3.0.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/3.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:3.0.0)

### Branch tags

- `latest` - branch `master`
- `develop` - branch `develop`

## Features

- [x] Base from `node:lts-alpine` image
- [x] Install latest `laravel-echo-server`
- [x] Auto generate config file

## Requirement
- Docker Engine 1.13+

## Usage

### Run laravel-echo-server

Run laravel-echo-server by command

```bash
$ docker run -d -p 6001:6001 -v $(pwd):/appoanhnn/laravel-echo-server
```


### Run laravel-echo-server sub-commands

```bash
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server init
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server start
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server client:add
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server client:remove
```

### Run with docker-compose

See some examples in `examples` folder.


### Auto generate config file

- If `/app/laravel-echo-server.json` is exists, it will be loaded
- If `/app/laravel-echo-server.json` isn't exists, it will be generated from default configs with [laravel-echo-server](https://github.com/tlaverdure/laravel-echo-server/blob/master/README.md#configurable-options). 
- If `/app/laravel-echo-server.json` isn't exists and you want it will be generated by another process, 
  please set environment variable `LARAVEL_ECHO_SERVER_GENERATE_CONFIG` to `false` (default `true`).   
  
  ```bash
  $ docker run -d -p 6001:6001 -v $(pwd):/app -e "LARAVEL_ECHO_SERVER_GENERATE_CONFIG=false" oanhnn/laravel-echo-server
  ```


### Configure database

The database may be `redis` of `sqlite`.   
It be configured by environment variable `LARAVEL_ECHO_SERVER_DB` (default is `redis`). 


- By default, Redis database will be used. You can set Redis config by environment variables:

  ```json
  "databaseConfig": {
    "redis": {
      "host": "REDIS_HOST",
      "port": "REDIS_PORT",
      "password": "REDIS_PASSWORD",
      "keyPrefix": "REDIS_PREFIX",
      "options": {
        "db": "REDIS_DB"
      }
    }
  },
  ```

  | Environment variable | Default value       |
  |:---------------------|:--------------------|
  | `REDIS_HOST`         | `redis`             |
  | `REDIS_PORT`         | `6379`              |
  | `REDIS_PASSWORD`     | `NULL`              |
  | `REDIS_PREFIX`       | `laravel_database_` |
  | `REDIS_DB`           | `0`                 |

- You can use SQLite database by set environment variable `LARAVEL_ECHO_SERVER_DB` to `sqlite`. 
  The SQLite file will store in `/app/database/`

  ```bash
  $ docker run -d -p 6001:6001 -v $(pwd):/app -e "LARAVEL_ECHO_SERVER_DB=sqlite" oanhnn/laravel-echo-server
  ```


### Override config by environment variables

If some environment variables are existed (allow load `/app/.env` file is found), the following options can be overridden:

| Environment variable                 | Config key                      | Note |
|:-------------------------------------|:--------------------------------|:-----|
| `LARAVEL_ECHO_SERVER_AUTH_HOST`      | `authHost`                      | This option will fall back to the `LARAVEL_ECHO_SERVER_HOST` option as the default if that is set. |
| `LARAVEL_ECHO_SERVER_HOST`           | `host`                          | |
| `LARAVEL_ECHO_SERVER_PORT`           | `port`                          | |
| `LARAVEL_ECHO_SERVER_DEBUG`          | `devMode`                       | |
| `LARAVEL_ECHO_SERVER_REDIS_HOST`     | `databaseConfig.redis.host`     | |
| `LARAVEL_ECHO_SERVER_REDIS_PORT`     | `databaseConfig.redis.port`     | |
| `LARAVEL_ECHO_SERVER_REDIS_PASSWORD` | `databaseConfig.redis.password` | |
| `LARAVEL_ECHO_SERVER_PROTO`          | `protocol`                      | |
| `LARAVEL_ECHO_SERVER_SSL_KEY`        | `sslKeyPath`                    | |
| `LARAVEL_ECHO_SERVER_SSL_CERT`       | `sslCertPath`                   | |
| `LARAVEL_ECHO_SERVER_SSL_PASS`       | `sslPassphrase`                 | |
| `LARAVEL_ECHO_SERVER_SSL_CHAIN`      | `sslCertChainPath`              | |

See more about environment variables in [here](https://github.com/tlaverdure/laravel-echo-server/blob/master/README.md#dotenv)


## Contributing

All code contributions must go through a pull request and approved by a core developer before being merged. 
This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-laravel-echo-server/issues).

## License

This project is released under the MIT License.   
Copyright © [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-laravel-echo-server/blob/master/LICENSE) for more information.
