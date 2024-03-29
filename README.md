# VNC Library for Go
go-vnc is a VNC client library for Go.

This library implements [RFC 6143][RFC6143] -- The Remote Framebuffer Protocol
-- the protocol used by VNC.

## Project links
* Build Status:  [![Build Status][CIStatus]][CIProject]
* Documentation: [![GoDoc][GoDocStatus]][GoDoc]

## Setup
1. Download software and supporting packages.

    ```
    $ go get github.com/18121861183/go-vnc
    $ go get golang.org/x/net
    ```

## Usage
Sample code usage is available in the GoDoc.

- Connect and listen to server messages: <https://godoc.org/github.com/18121861183/go-vnc#example-Connect>

The source code is laid out such that the files match the document sections:

- [7.1] handshake.go
- [7.2] security.go
- [7.3] initialization.go
- [7.4] pixel_format.go
- [7.5] client.go
- [7.6] server.go
- [7.7] encodings.go

There are two additional files that provide everything else:

- vncclient.go -- code for instantiating a VNC client
- common.go -- common stuff not related to the RFB protocol

## Example
 ```
nc, err := net.Dial("tcp", "192.168.9.93:5900")
if err != nil {
    log.Fatalf("Error connecting to VNC host. %v", err)
}

// Negotiate connection with the server.
vcc := vnc.NewClientConfig("11111111")
vc, version, err := vnc.Connect(context.Background(), nc, vcc)

print(version)
if err != nil {
    log.Fatalf("Error negotiating connection to VNC host. %v", err)
}
fmt.Println(vc.DesktopName())
 ```

<!--- Links -->
[RFC6143]: http://tools.ietf.org/html/rfc6143

[CIProject]: https://travis-ci.org/18121861183/go-vnc
[CIStatus]: https://travis-ci.org/18121861183/go-vnc.png?branch=master

[GoDoc]: https://godoc.org/github.com/18121861183/go-vnc
[GoDocStatus]: https://godoc.org/github.com/18121861183/go-vnc?status.svg
