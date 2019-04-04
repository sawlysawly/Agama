# Agama Wallet
Komodos Desktop Multicoin Wallet

## Build & Installation

#### Prerequirements:

1) [Install nodeJS](https://nodejs.org/en/download/package-manager/)/npm

2) Install git
```shell
 apt-get install git
```

#### Build & Start EasyDEX-GUI (frontend)

```shell
git clone --recursive https://github.com/komodoplatform/agama --branch master --single-branch
cd agama/gui/EasyDEX-GUI/react/
git checkout master && git pull origin master
npm update && npm install
npm run build && npm start
```
Leave the above process running and use a new terminal windows/tab when proceeding with the below steps.

Now please create a directory called `bin` inside `assets/` and afterwards copy `komodod` and `komodo-cli` to a new subfolder named after the operating system you are building Agama for: `linux64`, `osx` or `win64`. 
From within `agama/` the structure will be `assets/bin/linux64` (for example on linux).


#### Start Agama App (electron)

```shell
cd agama
npm update && npm install
npm start
```
In order to use debug/dev mode please stop Agama App (electron) and either set `dev: true` and `debug: true` in `~/.agama/config.json` and then restart the app or replace step 4) from above with the start command below:

```shell
npm start devmode
```

You re ready to dev!


## Bundling & packaging:

In order to build the release bundles please install the `electron-packager` and `electron-prebuilt` packages:

```shell
npm install electron-packager --save-dev
npm install electron-prebuilt --save-dev
```
We refer to the original [electron-packager](https://github.com/electron-userland/electron-packager) repository for more detailed information and further documentation.

#### Linux

```shell
cd agama
./node_modules/.bin/electron-packager . --platform=linux --arch=x64 --icon=assets/icons/agama_icons/128x128.png --out=build/ --buildVersion=VERSION_NUMBER_HERE --ignore=assets/bin/win64 --ignore=assets/bin/osx --overwrite
```
change architecture build parameter to ```--arch=x32``` for 32 bit build

#### OSX

```shell
cd agama
./node_modules/.bin/electron-packager . --platform=darwin --arch=x64 --icon=assets/icons/agama_icons/agama_app_icon.icns --out=build/ --buildVersion=VERSION_NUMBER_HERE --ignore=assets/bin/win64 --ignore=assets/bin/linux64 --overwrite
```

#### Windows

```shell
dir agama
./node_modules/.bin/electron-packager.exe . --platform=win32 --arch=x64 --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=VERSION_NUMBER_HERE --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite

# 32bit
electron-packager . --platform=win32 --arch=ia32 --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=VERSION_NUMBER_HERE --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite

# x64 and x86
electron-packager . --platform=win32 --arch=all --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=VERSION_NUMBER_HERE --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite
```

## Additional bundling tools for deb and rpm packages

[electron-installer-debian](https://github.com/electron-userland/electron-installer-debian)
[electron-installer-redhat](https://github.com/electron-userland/electron-installer-redhat)
