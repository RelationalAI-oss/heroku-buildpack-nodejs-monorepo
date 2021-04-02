# heroku-buildpack-nodejs-monorepo
This is an Heroku buildpack supporting deployment of Node.js applications within a monorepo, where the application
might make use of shared resources outside its subdirectory tree within the monorepo.

This is based on the example of
[Heroku Multi Procfile buildpack](https://github.com/heroku/heroku-buildpack-multi-procfile),
extending that to include the copying of the application's `package.json` and `package-lock.json`
files to Heroku's root application compilation directory.

The buildpack expects to find an environment variable, `APP_BASE`, which points to the
relative path of the application directory within the monorepo.

It also expects to find the `Procfile`, `package.json`, and `package-lock.json`
files within the `APP_BASE` directory.

The `Procfile` should look like this where `$APP_BASE` points to `appdir`:
```
web: cd appdir && node path/to/app-start.js
```
