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
After pulling the tailwind intellisense repo and debugging it with this repo in the vs code extension host,
I console logged the initial error:

```
Locating server…
Checking if /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css may be Tailwind-related…
Booting server...
Debugger listening on ws://127.0.0.1:6011/98fc5a5c-da2c-405d-aee1-3014ef6a571b
For help, see: https://nodejs.org/en/docs/inspector
Setting up server…
Listening for messages…
Searching for Tailwind CSS projects in the workspace's folders.
{"tailwind":{"version":"4.0.6","features":["css-at-theme","layer:base","content-list"],"isDefaultVersion":true},"path":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css"}
[Global] Creating projects: [{"folder":"/Users/ryan/tailwind-intellisense-bug-repro","config":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css","selectors":[{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css","priority":0},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/**","priority":2},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/**","priority":4},{"pattern":"/Users/ryan/tailwind-intellisense-bug-repro/**","priority":5}],"user":false,"tailwind":{"version":"4.0.6","features":["css-at-theme","layer:base","content-list"],"isDefaultVersion":true}}]
[Global] Preparing projects...
[Global] Initializing projects...
[app/assets/tailwind/application.css] Initializing...
[Global] Adding watch patterns: /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/application.css, /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind, /Users/ryan/tailwind-intellisense-bug-repro/app/assets, /Users/ryan/tailwind-intellisense-bug-repro/app, /Users/ryan/tailwind-intellisense-bug-repro
[app/assets/tailwind/application.css] Failed to load workspace modules.
[app/assets/tailwind/application.css] Using bundled version of `tailwindcss`: v4.0.6
[app/assets/tailwind/application.css] Building...
Error: Can't resolve 'tailwindcss' in '/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind'
    at finishWithoutResolve (/Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:2939:25)
    at /Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:3023:26
    at /Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:3073:13
    at eval (eval at create (/Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:1542:19), <anonymous>:15:1)
    at /Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:3073:13
    at eval (eval at create (/Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:1542:19), <anonymous>:16:1)
    at /Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:3073:13
    at eval (eval at create (/Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:1542:19), <anonymous>:15:1)
    at /Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:3073:13
    at eval (eval at create (/Users/ryan/tailwindcss-intellisense/packages/vscode-tailwindcss/dist/server.js:1542:19), <anonymous>:15:1) {
  details: "resolve 'tailwindcss' in '/Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind'\n" +
    '  Parsed request is a module\n' +
    '  No description file found in /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind or above\n' +
    '  No description file found in /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind or above\n' +
    '  no extension\n' +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/tailwindcss doesn't exist\n" +
    '  .css\n' +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/tailwindcss.css doesn't exist\n" +
    '  as directory\n' +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/tailwindcss doesn't exist\n" +
    '  resolve as module\n' +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/assets/tailwind/node_modules doesn't exist or is not a directory\n" +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/assets/node_modules doesn't exist or is not a directory\n" +
    "    /Users/ryan/tailwind-intellisense-bug-repro/app/node_modules doesn't exist or is not a directory\n" +
    "    /Users/ryan/tailwind-intellisense-bug-repro/node_modules doesn't exist or is not a directory\n" +
    "    /Users/ryan/node_modules doesn't exist or is not a directory\n" +
    "    /Users/node_modules doesn't exist or is not a directory\n" +
    "    /node_modules doesn't exist or is not a directory"
}
[Error - 4:26:45 PM] Loading fallback stylesheet for: tailwindcss
[Global] Initialized 1 projects
```




