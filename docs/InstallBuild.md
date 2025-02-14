# Installing/Building Ligolo-ng

!!! info

    The ligolo-ng proxy has been tested on various architectures, and is expected to run on Windows, Linux, Mac, FreeBSD and OpenBSD.
    The agent, on the other hand, is very simple to use and should work on almost all Golang-supported architectures. With a little work, you should even be able to implement it in other languages!

## Precompiled binaries

Precompiled binaries (Windows/Linux/macOS/BSD) are available on the [Release page](https://github.com/nicocha30/ligolo-ng/releases).

## Kali Repository

Ligolo-ng is now included by default in Kali Linux. You can install it using `apt install ligolo-ng`. However, I recommend using the latest precompiled version on this github repository.

### Building Ligolo-ng
Building *ligolo-ng* (Go >= 1.20 is required):

```shell
$ go build -o agent cmd/agent/main.go
$ go build -o proxy cmd/proxy/main.go
# Build for Windows
$ GOOS=windows go build -o agent.exe cmd/agent/main.go
$ GOOS=windows go build -o proxy.exe cmd/proxy/main.go
```