# How to configure auto update for Electron using electron-builder

Create new public repo in Github and then configure the package.json is configure like this:

```json
{
  "name": "mycoolapp",
  "version": "1.0.1",
  "description": "My Cool App",
  "main": "index.js",
  "author": {
    "name": "Anthony",
    "email": "name@company.com"
  },
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "<URL of the public repo>"
  },
  "dependencies": {
    "electron-log": "^4.3.2",
    "tslib": "^2.0.0"
  },
  "devDependencies": {
    "electron": "^11.1.0"
  },
  "build": {
    "appId": "com.company.coolapp",
    "productName": "Reader",
    "copyright": "Copyright © 2018-2019",
    "asar": true,
    "npmRebuild": false,
    "directories": {
      "buildResources": "icons",
      "output": "../reader-packages"
    },
    "mac": {
      "category": "public.app-category.developer-tools",
      "icon": "icon.png",
      "publish": ["github"]
    },
    "win": {
      "target": "nsis",
      "icon": "icon.ico",
      "publish": ["github"]
    },
    "linux": {
      "icon": "icon.png",
      "target": ["AppImage", "deb", "tar.gz"],
      "synopsis": "My app",
      "category": "Development"
    },
    "files": [
      "**/*",
      "!**/*.ts",
      "!*.code-workspace",
      "!LICENSE.md",
      "!package.json",
      "!package-lock.json",
      "!src/",
      "!e2e/",
      "!hooks/",
      "!angular.json",
      "!_config.yml",
      "!karma.conf.js",
      "!tsconfig.json",
      "!tslint.json"
    ],
    "nsis": {
      "oneClick": false,
      "perMachine": true,
      "allowToChangeInstallationDirectory": true,
      "createDesktopShortcut": "always",
      "deleteAppDataOnUninstall": true,
      "include": "installer.nsh"
    },
    "publish": [
      {
        "provider": "github",
        "owner": "Anthony",
        "repo": "<name of the repo>"
      }
    ]
  }
}
```

Then:

1. get new GitHub token at `https://github.com/settings/tokens/new`
1. define environment variable called `GITHUB_TOKEN` by running `export GITHUB_TOKEN=xyz`
1. pump the version in the `/apps/electron/reader/src/package.json`
1. run `electron-builder --publish`
1. see https://github.com/iffy/electron-updater-example/blob/master/main.js for example of Electron updater in action
