# bd-edge-js

This is a fork of [electron-edge-js](https://github.com/agracio/electron-edge-js) (which is itself a fork of [edge-js](https://github.com/agracio/edge-js)) patched to support BetterDiscord.

Discord runs 32-bit Electron 1.7.9 (node v7.9.0) and calls `electron.app.setVersion` at the start, so the version property electron-edge-js looks for isn't there.

To fix this we simply use the deprecated (but still working) `process.versions['atom-shell']` property.

NB: Inspecting edge.js stuff with Chromium DevTools can sometimes crash the renderer process. Here be dragons!

Usage is the same as edge or edge-js, replace `require('edge')` or `require('edge-js')` with `require('electron-edge-js')`:

```bash
npm install bd-edge-js
```

```diff
-var edge = require('edge');
+var edge = require('bd-edge-js');

var helloWorld = edge.func(function () {/*
    async (input) => {
        return ".NET Welcomes " + input.ToString();
    }
*/});

// Do not attempt to dump `helloWorld` in DevTools. It will crash Electron!
```


## Why use `bd-edge-js`?

Discord's Electron is built using specific version of Node.js. In order to use `edge` in Electron project you would need to recompile it using the same Node.js version.

`bd-edge-js` comes precompiled with correct Node.js versions.

## Differences from `electron-edge`

* Uses same codebase as `edge-js` that comes with both latest code changes from `edge` project and additional fixes and improvements available in `edge-js` project.
* Supports majority of Electron versions.

## Differences from `electron-edge-js`

* 