<div align="center">
    <h1>Guark</h1>
    <p>Guark allows you to build beautiful user interfaces using modern web technologies such as Vue.js, React.js..., while your app logic handled and powered by the amazing <b>Go</b>.</p>
    <p align="center">
        <a href="#installation">Installation</a> ❘
        <a href="#getting-started">Getting Started</a> ❘
        <a href="#contributing">Contributing</a> ❘
        <a href="#license">License</a>
    </p>
</div>

![Guark Vue Template](https://i.imgur.com/RhU6bh7.png)



## 🖳  About The Project

Guark is an open-source framework to build cross platform desktop GUI applications.

### 📢 What Guark stands for?

Go + Quark = Guark

### 🔮 Guark mission

Simplify cross platform desktop apps development.

### 🎸 How it works

Demo Video: https://youtu.be/_k_tq9sj-do

Guark backend and logic part handled by native Go code, while the user interfaces built with modern web technologies (Vue.js, React.js, etc...), and with Guark javascript API you can communicate between your Go and UI framework, and calling your exported Go functions and plugin(s) methods.

## 💌  Main Features

- Desktop applications with GO ♥
- One codebase for Gnu/Linux, macOS, and Windows.
- UI Hot Reload.
- You can use any front end framework.
- Supports Chrome, and native webview engine or both.
- Windows MSI bundler builtin.


## 📜  Installation

#### 1. Install guark CLI tool:
```bash
go get -u github.com/guark/guark/cmd/guark
```

#### 2. Some Gnu/Linux ❤ Requirements:

```bash
// fedora
sudo dnf install gtk3-devel webkit2gtk3-devel gcc-c++ pkgconf-pkg-config

// Ubuntu
sudo apt install libgtk-3-dev libwebkit2gtk-4.0-dev build-essential
```

## Getting Started

After installing guark CLI tool, the next step is to create a new guark project based on the template that you like:

### Create a new project

```bash
# cd to empty directory and run:
guark init --template vue
```

### Start Dev Server

After creating new project run:
```bash
guark run
```

### Export your first GO function to JS API

##### 1. Create a new file in `lib/funcs` directory:
```go
// lib/funcs/foo_bar.go

import (
    "github.com/guark/guark/app"
)

func FooBar(c app.Context) (interface{}, error) {

   c.App.Log.Debug("Foo bar called")

   return "This is a my return value to javasript", nil
}
```

##### 2. Then export it to Guark JS API in `lib/config.go` file:

```go
// Exposed functions to guark Javascript api.
var Funcs = app.Funcs{
    "foo": funcs.FooBar,
}

```

##### 3. Then you can call your function in javascript:

```js
import g from "guark"

g.call("foo")
 .then(res => console.log(res))
 .catch(err => console.error(err))
```

See Vue template as an example: https://github.com/guark/vue

## Guark Engines:

You can change the engine in `guark.yaml` file.

- `webview`: Uses native system webview.
- `chrome`: Uses and requires google chrome.
- `hybrid`: Uses chrome if exists in the system, if chrome not available guark will switch to native webview by default.


## Build Your App

You can build your app with
```bash
guark build
```

## Bundle Windows App

After building your app you can bundle your windows app into msi using WIX.
```bash
guark bundle
```

## Cross Compiling To Windows From Gnu/Linux:

You can build windows app from your linux based system, using `mingw64`

#### 1. Install mingw64:
```bash
// Fedora
sudo dnf install mingw64-gcc

// Ubuntu
sudo apt install binutils-mingw-w64
```

#### 2. Configure `guark-build.yaml` File:

Double check the binary paths in `guark-build.yaml`.

#### 3. Build The App:

```bash
# this command will build and compile linux, and windows app. you can find your compiled apps in `dist/` directory.
guark build --target linux --target windows
```

You can use any cross compiler for example: `guark build --target darwin`. just change the options in `guark-build.yaml` file.

#### Note
You can also bundle windows app into MSI file from your linux based system via `guark bundle`, but you need to install wix tools:

```bash
# fedora
dnf install msitools

# Ubuntu
sudo apt-get install wixl
```

## Contributing

PRs, issues, and feedback from ninja gophers are very welcomed.

## License

Guark is provided under the [MIT License](https://github.com/guark/guark/blob/master/LICENSE).

