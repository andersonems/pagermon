# [PagerMon](https://hrng.io/)
![Discord](https://img.shields.io/discord/533900375066017812.svg?style=plastic)
![GitHub issues](https://img.shields.io/github/issues-raw/pagermon/pagermon.svg?style=plastic)
![GitHub pull requests](https://img.shields.io/github/issues-pr/pagermon/pagermon.svg?style=plastic)
![GitHub](https://img.shields.io/github/license/pagermon/pagermon.svg?style=plastic)
![GitHub stars](https://img.shields.io/github/stars/pagermon/pagermon.svg?style=plastic)
![GitHub forks](https://img.shields.io/github/forks/pagermon/pagermon.svg?style=plastic)
![GitHub tag (latest SemVer)](https://img.shields.io/github/tag/pagermon/pagermon.svg?label=release&style=plastic)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/pagermon/pagermon.svg?style=plastic)
![GitHub contributors](https://img.shields.io/github/contributors/pagermon/pagermon.svg?style=plastic)

PagerMon is an API driven client/server framework for parsing and displaying pager messages from multimon-ng.

It is built around POCSAG messages, but should easily support other message types as required.

The UI is built around a Node/Express/Angular/Bootstrap stack, while the client scripts are Node scripts that receive piped input.

## Features

* Capcode aliasing with colors and [FontAwesome](https://fontawesome.io/icons/) icons
* API driven extensible architecture
* Single user, multiple API keys
* SQLite or MySQL database backing
* Configurable via UI
* Pagination and searching
* Filtering by capcode or agency
* Duplicate message filtering
* Keyword highlighting
* WebSockets support - messages are delivered to clients in near realtime
* Pretty HTML5
* Native browner notifications
* Plugin Support - Current Plugins:
    * [Pushover](https://pushover.net/) near realtime muti-device notification service
    * [Telegram](https://telegram.org/) near realtime cloud based multi-device messaging
    * [Discord](https://discordapp.com/) near realtime cloud based messaging service
    * [Gotify](https://gotify.net/) Self-Hosted messaging service
    * [Twitter](www.twitter.com)
    * [Microsoft Teams](https://products.office.com/en-us/microsoft-teams/group-chat-software) Team colaboration platform
    * [Slack](https://slack.com/) Team colabortation platform
    * SMTP Email Support for conventional SMTP email notifications 
    * Regex Filters - Filter incoming messages via regex
    * Regex Replace - Modify incoming messages via regex
    * Message Repeat - Repeat incoming messages to another pagermon server
* May or may not contain cute puppies

### Planned Features

* Multi-user support
* Postgres + MariaDB Support
* Horizontal scaling
* Enhanced message filtering
* Bootstrap 4 + Angular 2 support
* Enhanced alias control
* Graphing
* Non-sucky documentation

### Screenshots

![main view](http://i.imgur.com/QWKoJjb.jpeg)

![desktop view](http://i.imgur.com/Zik74Dl.jpeg)

![alias edit](http://i.imgur.com/gus8QTe.jpeg)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

* [nodejs](https://nodejs.org/)
* sqlite3
* Probably some other stuff

#### Recommended

* [nvm](https://github.com/creationix/nvm#installation)
* nginx or some kind of reverse proxy for SSL offloading

## Running the server

### Local setup

1) Copy server/process-default.json to server/process.json and modify according to your environment
2) Launch the app from the Terminal:

```
    $ sudo apt-get install npm sqlite3
    $ npm install npm@latest -g
    $ npm install pm2 -g
    $ cd server
    $ npm install
    $ export NODE_ENV=production
    $ pm2 start process.json
```
3) To start on boot, let pm2 handle it:
```
    $ sudo pm2 startup
    $ pm2 save
```
4) You probably want to rotate logs, too:
```
    $ pm2 install pm2-logrotate
    $ sudo pm2 logrotate -u user
```
5) Now login via the website, default port is 3000, default credentials are 'admin' / 'changeme'
6) Head to /admin, change your password, and generate some API keys
6) Grab your API keys and drop them in the PagerMon client, then you're good to go!

Alternatively a production ready setup guide is available here
https://github.com/pagermon/pagermon/wiki/Setup-Guide---Ubuntu-Server-with-NGINX-Reverse-Proxy-and-Let's-Encrypt-SSL-Certificate


### Docker

1) Build the container:
```
    $ docker-compose build
```

2) Run the container

​	In __foreground__:
```
    $ docker-compose up 
```

OR

​	As __daemon__ (`-d`):
```
    $ docker-compose up -d
```
__NOTE:__
   - The database will be located relativ to your current working directory under `./data/messages.db` (by `-v $(pwd)/data:/data`)
   - The local port `3000` will be forwarded to the docker container to port `3000` (by `-p 3000:3000`)
   - In case you would like to follow the logfile, run `docker logs -f pagermon` (by `--name pagermon `)
   - To shutdown and remove the container, run `docker-compose down`
   - If you make changes to the app for testing, you will need to re-build the image, run `docker-compose down && docker-compose up --build`

3) Follow __Step 5__ from __Running the server____

## Support 

General PagerMon support can be requested in the #support channel of the PagerMon discord server.

[Click Here](https://discord.gg/3VK7gSD) to join

Bugs and Feature requests can be logged via the GitHub issues page. 

## Contributing

All are welcome to contribute. Contributors should submit a pull request with the requested changes.

CHANGELOG.md is to be updated on each pull request.

If a pull request is the first pull request since a [release](https://github.com/pagermon/pagermon/releases), then the version number should be bumped in `CHANGELOG.md`, `server/app.js`, and `server/package.json`.

If a database schema change is required, this must be done using KnexJS Migration files. **Insert Instructions for this here**

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/pagermon/pagermon/tags).

## Authors

See the list of [contributors](https://github.com/pagermon/pagermon/contributors) who participated in this project.

## License

This project is licensed under The Unlicense - because fuck licenses. Do what you want with it. :>

## Acknowledgments

* [multimon-ng](https://github.com/EliasOenal/multimon-ng)
