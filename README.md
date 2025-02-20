# README

Development setup:

- clone repository
- run `bundle install`
- run `bin/dev` to start the server + Tailwind

Or from scratch:

- `rails new YOUR_APP_NAME`
- `cd YOUR_APP_NAME`
- `./bin/bundle add tailwindcss-rails`
- `./bin/rails tailwindcss:install`
- `rails g controller home index`
- `bin/dev`

Bug repro:

Using versions: 

- tailwindcss-intellisense 0.14.6
- tailwindcss-rails 4.1.0
- tailwindcss-ruby 4.0.7

Check vscode output for tailwind intellisense after loading the IDE window. Will display logs:

```Locating server…
Booting server...
Starting inspector on 127.0.0.1:6011 failed: address already in use
Setting up server…
Listening for messages…
Searching for Tailwind CSS projects in the workspace's folders.
{"tailwind":{"version":"4.0.6","features":["css-at-theme","layer:base","content-list"],"isDefaultVersion":true},"path":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css"}
[Global] Creating projects: [{"folder":"/Users/ryan/tailwind-intellisense-bug-repro","config":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css","selectors":[{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css","priority":0},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/**","priority":2},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/**","priority":4},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/**","priority":5}],"user":false,"tailwind":{"version":"4.0.6","features":["css-at-theme","layer:base","content-list"],"isDefaultVersion":true}}]
[Global] Preparing projects...
[Global] Initializing projects...
[Global] Initialized 0 projects
[app/assets/tailwind/application.css] Initializing...
[Global] Adding watch patterns: /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css, /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind, /Users/ryan/tailwind-intellisense-bug-repro/app/assets, /Users/ryan/tailwind-intellisense-bug-repro/app, /Users/ryan/tailwind-intellisense-bug-repro
[app/assets/tailwind/application.css] Failed to load workspace modules.
[app/assets/tailwind/application.css] Using bundled version of `tailwindcss`: v4.0.6
[app/assets/tailwind/application.css] Building...
[Error - 4:09:14 PM] Loading fallback stylesheet for: tailwindcss
```



