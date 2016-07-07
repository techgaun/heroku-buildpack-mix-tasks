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

Note: Right now, [HashNuke/heroku-buildpack-elixir](https://github.com/HashNuke/heroku-buildpack-elixir) does not export paths of previous buildpacks in sequence for subsequent buildpacks so you might need to use [techgaun/heroku-buildpack-elixir](https://github.com/techgaun/heroku-buildpack-elixir) in some cases.

### Configuration

Configure the `MIX_DEPLOY_TASKS` environment variable with the tasks you want to run.

```shell
heroku config:set MIX_DEPLOY_TASKS='ecto.migrate'
```

You can separate tasks with semicolon if you want to run multiple tasks. Note that they will run in a sequential order.

```shell
heroku config:set MIX_DEPLOY_TASKS='ecto.drop;ecto.create;ecto.migrate'
```

On a side note, I do not recommend running `ecto.migrate`, db related commands and other various time consuming commands on Production. Esp. running `ecto.migrate` on Production can become a nightmare when you have grown to big database.

## License
MIT
