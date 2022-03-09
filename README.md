# FreeTDS / gobject-introspection on Heroku Minimum Reproducible Example

## What?

This is a Rails application demonstrating a minimum reproducible example of a
Heroku buildpacks interaction bug where the Rails application can be deployed
correctly to Heroku, but the application will not boot.

```
/app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require': libgirepository-1.0.so.1: cannot open shared object file: No such file or directory - /app/vendor/bundle/ruby/3.1.0/gems/gobject-introspection-3.5.1/lib/gobject_introspection.so (LoadError)
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/bundle/ruby/3.1.0/gems/gobject-introspection-3.5.1/lib/gobject-introspection.rb:34:in `<main>'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler/runtime.rb:60:in `block (2 levels) in require'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler/runtime.rb:55:in `each'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler/runtime.rb:55:in `block in require'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler/runtime.rb:44:in `each'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler/runtime.rb:44:in `require'
        from /app/vendor/ruby-3.1.0/lib/ruby/3.1.0/bundler.rb:176:in `require'
        from /app/config/application.rb:19:in `<main>'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/command/actions.rb:22:in `require_application!'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/command/actions.rb:14:in `require_application_and_environment!'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/commands/console/console_command.rb:101:in `perform'
        from /app/vendor/bundle/ruby/3.1.0/gems/thor-1.2.1/lib/thor/command.rb:27:in `run'
        from /app/vendor/bundle/ruby/3.1.0/gems/thor-1.2.1/lib/thor/invocation.rb:127:in `invoke_command'
        from /app/vendor/bundle/ruby/3.1.0/gems/thor-1.2.1/lib/thor.rb:392:in `dispatch'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/command/base.rb:87:in `perform'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/command.rb:48:in `invoke'
        from /app/vendor/bundle/ruby/3.1.0/gems/railties-7.0.2.3/lib/rails/commands.rb:18:in `<main>'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from /app/vendor/bundle/ruby/3.1.0/gems/bootsnap-1.11.1/lib/bootsnap/load_path_cache/core_ext/kernel_require.rb:30:in `require'
        from bin/rails:4:in `<main>'
```

This uses an Aptfile to install libgirepository, and separately a Heroku
buildpack to install FreeTDS to connect to MSSQLServer.

## Heroku Buildpacks

```
=== {appname} Buildpack URLs
1. heroku-community/apt
2. https://github.com/rails-sqlserver/heroku-buildpack-freetds#v1.1.2
3. heroku/ruby
```
