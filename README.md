# Sidekiq Web UI example using GitHub OAuth

Do you want to use the [Sidekiq](http://sidekiq.org) Web UI as a standalone app, using GitHub OAuth for authentication? Then this app is just for you. It's ready to be deployed on Heroku, so if that's your thing, you're all settled.

## Setup

### Basics
1. `git clone git@github.com:teamcocoon/sidekiq-github-example.git`
2. `bundle install`

### Add GitHub OAuth
1. [Create a new OAuth application](https://github.com/settings/applications/new)
2. Use `/auth/github/callback` as the authorization callback URL

### Configure
* To run it locally, fill in all the ENV variables in `.env`
* The `GITHUB_CLIENT_*` ones can be copied from your OAuth app page at GitHub
* `GITHUB_ORG` is the name of the GitHub organisation that you want to allow users from (as used in the URL on GitHub, e.g. http://github.com/teamfoo means `teamfoo` is your organisation name)
* For `RACK_SESSION_COOKIE` and `WARDEN_GITHUB_VERIFIER_SECRET` you need to create **two separate** secret session cookies with `openssl rand -base64 4`

_It's best practice not to commit the real values for these secrets to your repository_

### Run
* `rackup config.ru` or `heroku local`

### Deploy
This assumes you're deploying to Heroku and you've got the [Heroku Toolbelt](http://toolbelt.heroku.com) already installed.

1. Create a new app: `heroku create`
2. Set all the above ENV variables, e.g. `heroku config:set GITHUB_ORG=teamfoo`
3. Add the additional ENV variable for the Redis instance used by your Sidekiq Worker. If that worker is also on Heroku, you can copy the value from the ENV var `REDIS_PROVIDER` in that app. `heroku config:set REDIS_PROVIDER=http://example.com`
4. `git push heroku master`

Happy Monitoring 🔬
