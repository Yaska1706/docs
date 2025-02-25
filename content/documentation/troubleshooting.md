---
name: Troubleshooting
icon: "images/troubleshoot.svg"
aliases:
  - /en/docs/troubleshooting
---

# Troubleshooting

{{< faq "App Crashes with `securecookie: hash key is not set`" "securecookie-hash-key-not-set">}}
After a recent change in the [github.com/gorilla/sessions](http://www.gorillatoolkit.org/pkg/sessions) Buffalo applications will fail to start with the error `securecookie: hash key is not set`. To fix this you must set an environment variable named `SESSION_SECRET`.

For information see [https://github.com/gobuffalo/buffalo/issues/1067](https://github.com/gobuffalo/buffalo/issues/1067)
{{< /faq >}}
      
{{< faq "Command line is slow" "slow-commands">}}
If executing `buffalo --help` or any other command from the terminal takes longer than expected set `export BUFFALO_PLUGIN_PATH=$GOPATH/bin` in your shell config (e.g. .bash_profile).
{{< /faq >}}


{{< faq "Can't find `buffalo` binary." "binary-not-found">}}
If you can't find the `buffalo` binary after a successful installation, this is problably caused because `$GOPATH/bin`, or `%GOPATH\bin` (Windows), isn't in your `$PATH` variable. When a Go binary is installed it is placed in `$GOPATH/bin`. Adding this to your global `$PATH` will allow you to find **any** Go binary everywhere in your system. See [https://golang.org/doc/code.html#GOPATH](https://golang.org/doc/code.html#GOPATH) for more details.
{{< /faq >}}

{{< faq "`buffalo new` fails to generate a complete project." "failed-to-gen">}}
This happens because the `buffalo new` command cannot find the templates it needs to generate a new application.


There are a couple of things that could cause this issue.

* Using multiple `$GOPATH`s. This can happen when you install Buffalo to one `$GOPATH` and then create a new, temporary, `$GOPATH` and try to create a new application there. Because the templates are in the first, original `$GOPATH`, the installer does not find them, and subsequently generates an incomplete application. To fix this, use just one `$GOPATH`.
* Using a single `$GOPATH`. If you aren't using multiple `$GOPATH`s and are still seeing this issue, it is most likely caused by a bad installation. Run `$ go get -u -v github.com/gobuffalo/buffalo/buffalo` again, and it should, hopefully, repair the installation for you.

The original ticket for this issue can be found at [https://github.com/gobuffalo/buffalo/issues/629](https://github.com/gobuffalo/buffalo/issues/629).
{{< /faq >}}

{{< faq "`buffalo new` fails with NPM permissions issues." "npm-permissions">}}
This is caused by incorrectly setup Node/NPM installation. See <a href="https://docs.npmjs.com/getting-started/fixing-npm-permissions" target="_blank">docs.npmjs.com/getting-started/fixing-npm-permissions</a> for information on how to fix this issue.
{{< /faq >}}


{{< faq "`buffalo dev` auto rebuild doesn't work with NFS." "nfs-rebuild">}}
This is caused by the `fsnotify` package not supporting NFS. See <a href="https://github.com/gobuffalo/buffalo/issues/620" target="_blank">github.com/gobuffalo/buffalo/issues/620</a> for more details and a workaround.
{{< /faq >}}

{{< faq "`buffalo new` fails with `import path does not begin with hostname`" "import-begins-hostname">}}
This is caused by a mismatched `$GOPATH` and file system.


```
GOPATH: /Users/foobar/Documents/Programming/Go
ACTUAL: /Users/foobar/Documents/programming/go
```

Those are not the same and cause problems with a lot of Go tools. Correct the `$GOPATH` to match the file system and retry.
{{< /faq >}}

{{< faq "`buffalo new` fails looking for `golang.org/x/tools/go/gcimporter`" "gcimporter">}}
This is caused by an outdated copy of the `github.com/motemen/gore` package. To fix simply update `gore`:


```text
$ go get -u github.com/motemen/gore
```

For information see [https://github.com/gobuffalo/buffalo/issues/108](https://github.com/gobuffalo/buffalo/issues/108) and [https://github.com/motemen/gore/issues/63](https://github.com/motemen/gore/issues/63).
{{< /faq >}}

{{< faq "`buffalo dev` fails to start with `Unknown`" "fails-unknown">}}
When starting `$ buffalo dev`, and you encounter this error:


```text
There was a problem starting the dev server: Unknown, Please review the troubleshooting docs.
```

This may be due to your system missing NodeJS/NPM, Ensure that Node/NPM is installed and is in your `$PATH`. If  Node/NPM are indeed in your `$PATH`, try renaming webpack.config.js.

If you are still having issues after attempting the steps above, please reach out to the community in the #buffalo channel on Gophers Slack.
{{< /faq >}}

{{< faq "`package context: unrecognized import path \"context\" (import path does not begin with hostname)`" "unrecognized-context-import">}}
When trying to install Buffalo `go get` returns this error:


```text
package context: unrecognized import path "context" (import path does not begin with hostname)
```

This is due to an outdated version of Go. Buffalo requires Go 1.7 or higher. Please check your installation of Go and ensure you running the latest version.
{{< /faq >}}

{{< faq "Error: `unexpected directory layout:` during `go get`" "unexpected-dir-layout">}}
Occasionally when running `go get` on Buffalo you will get the following error:


```text
unexpected directory layout:
import path: github.com/mattn/go-colorable
dir: /go/src/github.com/fatih/color/vendor/github.com/mattn/go-colorable
expand dir: /go/src/github.com/fatih/color/vendor/github.com/mattn/go-colorable
separator: /
```

This issue has been reported previously the Go team, [github.com/golang/go/issues/17597](https://github.com/golang/go/issues/17597).

The best way to solve this problem is to run `go get` again, and it seems to fix itself.
{{< /faq >}}

{{< faq "Error: in `application.js` from UglifyJs" "appjs-uglify">}}
If you get this error when running `buffalo build` you need to update your `webpack.config.js` to work with [https://github.com/gobuffalo/buffalo/pull/350/files](https://github.com/gobuffalo/buffalo/pull/350/files).

{{< /faq >}}

{{< faq "Error: `Killed 9` when running `buffalo` on Mac OS X with Go 1.8.0" "mac-killed9">}}
This is a known issue with Go, <a href="https://github.com/golang/go/issues/19734" target="_blank">github.com/golang/go/issues/19734</a>, not with Buffalo.


The best solution is to upgrade to Go 1.8.1, or greater, and rebuild your Go binaries.
{{< /faq >}}

{{< faq "Mac OS X: `Too many open files in system` error" "mac-too-many-files">}}
If you get this error when running `buffalo dev` that means you are "watching" too many files, either `.go` files or asset files. To correct this you can [change](http://blog.mact.me/2014/10/22/yosemite-upgrade-changes-open-file-limit) the maximum number of open files on your system.

{{< /faq >}}

{{< faq "`buffalo new` fails trying to run `goimports`" "new-goimports">}}
The full error may appear something like the following, and seems to be the result of outdated go tools. To resolve run `rm -r $GOPATH/src/golang.org/`, then run `go get` again.

```bash
$ buffalo new myapp

--> go get -u golang.org/x/tools/cmd/goimports
package golang.org/x/tools/cmd/goimports: golang.org/x/tools is a custom import path for https://go.googlesource.com/tools, but /Users/foo/go/src/golang.org/x/tools is checked out from https://code.google.com/p/go.tools

Error: exit status 1
```
{{< /faq >}}

{{< faq "`buffalo g goth` fails to generate `auth.go`" "goth-auth-fails">}}
You might see errors similar to this when you build:

```bash
buffalo: 2018/01/19 20:58:47 === Error! ===
buffalo: 2018/01/19 20:58:47 === exit status 2
path/path/models
path/path/actions
# path/path/actions
actions/app.go:17:2: gothic redeclared as imported package name
    previous declaration at actions/app.go:15:2
actions/app.go:66:36: undefined: AuthCallback
actions/app.go:67:11: undefined: SetCurrentUser
actions/app.go:68:11: undefined: Authorize
actions/app.go:69:23: undefined: Authorize
```

This could be because the `goth` plugin isn't able to find the templates for the different providers. This can happen when the `goth` plugin is available in `$PATH`, but the project isn't in your current `$GOPATH`.

To fix it, you can either `go get -u github.com/gobuffalo/buffalo-goth` in your project's `$GOPATH` or use `dep`.
{{< /faq >}}
