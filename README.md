# heroku-buildpack-mix-tasks
> A simple buildpack that just runs mix commands on deployment

## Instruction

This buildpack is intended to be used after [heroku buildpack for elixir](https://github.com/HashNuke/heroku-buildpack-elixir) to run arbitrary commands during deployment.

### Usage

Make sure your app has heroku-buildpack-elixir configured.

```shell
heroku create --buildpack "https://github.com/HashNuke/heroku-buildpack-elixir.git" # for new app

heroku config:set BUILDPACK_URL="https://github.com/HashNuke/heroku-buildpack-elixir.git" # for existing app
```

Set this buildpack after the heroku-buildpack-elixir.

```shell
# Set the buildpack for your Heroku app
heroku buildpacks:set https://github.com/techgaun/heroku-buildpack-mix-tasks.git

# Add this buildpack after the Elixir buildpack
heroku buildpacks:add --index 1 https://github.com/HashNuke/heroku-buildpack-elixir.git
```

### Configuration

Configure the `MIX_DEPLOY_TASKS` environment variable with the tasks you want to run.

```shell
heroku config:set MIX_DEPLOY_TASKS='ecto.migrate'
```

## License
MIT
