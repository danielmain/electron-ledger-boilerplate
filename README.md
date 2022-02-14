# Electron application boilerplate using ledger hardware wallet

**electron-ledger-boilerplate**

A starter for a React based Electron app using ledger hardware wallet.

## How to use

```
yarn dev
```

To start the development version with hot module reloading.

```
yarn electron
```

To build the distributable application.

All bundled code will be in the build folder, the distributable App will be in dist.

The preload js is used to expose code from the main process in the renderer. Extend as needed by your app (don't forget to update the type definition in scr/@types/global.d.ts)

## Folder Structure

| Folder | Description                                                                     |
| ------ | ------------------------------------------------------------------------------- |
| config | Holds config for the app - currently just jest                                  |
| build  | Folder created by parcel for the bundled code                                   |
| dist   | Folder created by electron-builder for the finished electron app distributables |
| src    | All source code goes here                                                       |

The src folder contains:

| Folder   | Description                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------- |
| @types   | Type definitions for the window object - set in the src/main/preload.js                                     |
| locales  | Translation files used by react-i18next                                                                     |
| main     | Contains code for Electron's main process - it is what creates the electron window                          |
| renderer | Contains code for Electron's renderer process - this is where all your frontend code goes to create the App |

### src/main/preload.js

This script is used by electron to give access to main process imports or to create functions that you want to access in the renderer process. As an example some fs functions are added to the renderer's window object to allow loading of the localisation files.

I'm not sure if this is correcly setup - the only other app I made for electron was years ago and the renderer had access to all fs functions out-of-the-box(see my school-report repo), maybe something has changed with electon since then as the preload script was the only way I found to access node's fs module in the renderer.

## Scripts

| Command        | Description                                                        |
| -------------- | ------------------------------------------------------------------ |
| build:main     | Bundle the main TS for release                                     |
| build:renderer | Bundle the renderer TS for release                                 |
| build          | Parcel will bundle everything for release                          |
| clean:build    | Removes all files from build/                                      |
| clean:dist     | Removes all files from dist/                                       |
| copy:preload   | Copy the preload script used by electron to the build folder       |
| dev:bundle     | Concurrently runs dev:main and dev:renderer                        |
| dev:main       | Bundle the main TS                                                 |
| dev:renderer   | Bundle and watch the renderer TS and start Parcel's dev server     |
| dev:wait       | Waits for the main TS to bundle and dev server to start            |
| dev            | Develop the electron app - Parcel will start a server with HMR     |
| electron       | Build the electron app - Parcel will bundle everything for release |
| lint:js        | Lint JS/TS with ESLint and fix errors                              |
| lint:prettier  | Lint JS/TS with Prettier                                           |
| lint:ts        | Lint TS files                                                      |
| lint           | Run all linters                                                    |
| release        | Increases version and updates change log and creates a tag         |
| test           | Run tests using jest                                               |