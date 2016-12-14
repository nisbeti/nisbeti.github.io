---
layout: default
title: npm WARN deprecated ...
---
When running ```npm install``` with Laravel, we often see these Warnings:

```
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated minimatch@0.2.14: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated graceful-fs@1.2.3: graceful-fs v3.0.0 and before will fail on node releases >= v7.0. Please update to graceful-fs@^4.0.0 as soon as possible. Use 'npm ls graceful-fs' to find it in the tree.
```

A little research revealed the following:

The ```minimatch``` warnings are due to Gulp being in the process of being updated at the moment, as they are caused by it depending on some old dependencies, which in turn depend upon these soon to be deprecated package versions.

The most useful thread is at [https://github.com/Polymer/polymer-cli/issues/381](https://github.com/Polymer/polymer-cli/issues/381)
While there is further discussion on Gulp update progress at [https://github.com/gulpjs/gulp/issues/1604](https://github.com/Polymer/polymer-cli/issues/381)
It appears that, as long as no user input (untrusted) is being passed into Gulp, then there is no actual security risk.

Running the following command:

```
npm ls minimatch
```

In a Spark root directory reveals:

```
+-- gulp@3.9.1
| `-- vinyl-fs@0.3.14
| +-- glob-stream@3.1.18
| | `-- minimatch@2.0.10
| `-- glob-watcher@0.0.6
| `-- gaze@0.5.2
| `-- globule@0.1.0
| `-- minimatch@0.2.14
`-- laravel-elixir@6.0.0-11
`-- glob@7.1.1
`-- minimatch@3.0.3
```

And, running the following command:

```
npm ls graceful-fs
```

Reveals:

```
+-- gulp@3.9.1
| `-- vinyl-fs@0.3.14
| +-- glob-watcher@0.0.6
| | `-- gaze@0.5.2
| | `-- globule@0.1.0
| | `-- glob@3.1.21
| | `-- graceful-fs@1.2.3
| `-- graceful-fs@3.0.11
+-- laravel-elixir@6.0.0-11
| +-- gulp-less@3.1.0
| | +-- accord@0.23.0
| | | `-- fobject@0.0.4
| | | `-- graceful-fs@4.1.9
| | `-- less@2.7.1
| | `-- graceful-fs@4.1.9
| +-- gulp-rev@7.1.2
| | `-- vinyl-file@1.3.0
| | `-- graceful-fs@4.1.9
| +-- gulp-sass@2.3.2
| | `-- node-sass@3.10.1
| | `-- node-gyp@3.4.0
| | +-- fstream@1.0.10
| | | `-- graceful-fs@4.1.9
| | `-- graceful-fs@4.1.9
| `-- gulp-sourcemaps@1.9.0
| `-- graceful-fs@4.1.9
`-- laravel-elixir-webpack-official@1.0.9
`-- webpack@2.1.0-beta.22
+-- enhanced-resolve@2.3.0
| `-- graceful-fs@4.1.9
+-- watchpack@1.1.0
| +-- chokidar@1.6.1
| | `-- readdirp@2.1.0
| | `-- graceful-fs@4.1.9
| `-- graceful-fs@4.1.9
`-- yargs@4.8.1
`-- read-pkg-up@1.0.1
`-- read-pkg@1.1.0
+-- load-json-file@1.1.0
| `-- graceful-fs@4.1.9
`-- path-type@1.1.0
`-- graceful-fs@4.1.9
```
