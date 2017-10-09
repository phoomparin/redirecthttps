<div align="center">
  <img src="logo.png" alt="Logo" width='45%' />

  <h2>RedirectHTTPS: HTTPS Redirection Middleware</h2>
  <p>A minimalistic middleware that redirects all network traffic from the insecure HTTP protocol to the HTTPS transport, all written in Go<p>
</div>

<br />

<div align="center">

[![Go Report Card](https://goreportcard.com/badge/github.com/acoshift/redirecthttps?style=flat-square)](https://goreportcard.com/report/github.com/acoshift/redirecthttps)
[![build status](https://img.shields.io/travis/acoshift/redirecthttps/master.svg?style=flat-square)](https://travis-ci.org/kataras/iris)
[![github issues](https://img.shields.io/github/issues/acoshift/redirecthttps.svg?style=flat-square)](https://github.com/acoshift/redirecthttps/issues?q=is%3Aopen+is%3Aissue)
[![release](https://img.shields.io/github/release/acoshift/redirecthttps.svg?style=flat-square)](https://github.com/acoshift/redirecthttps/releases)
[![chat](https://img.shields.io/badge/community-%20chat-00BCD4.svg?style=flat-square)](https://gitter.im/acoshift)
[![license](https://img.shields.io/github/license/acoshift/redirecthttps.svg?style=flat-square)]()

</div>

<br />

### Installation

`go get github.com/acoshift/redirecthttps`

### Usage Example

This middleware can be applied in the middleware chain, as follows:

```
middlewares := middleware.Chain(
  // We can put our redirection middleware right here.
  redirecthttps.New(redirecthttps.Config{
    // The redirection mode can be specified below.
    Mode: redirecthttps.OnlyProxy
  }),
)

mux.Handle("/", middlewares(app.Handler()))
```

### Configuration: Redirection Modes

There are three redirection modes, which can be specified before instantiating the middleware.

First, the `OnlyConnectionState` Mode, which only checks the connection state from request.TLS, and perform the redirection if TLS is not present in the request.

Second, the `OnlyProxy` Mode, which only checks the X-Forwarded-Proto header from the request in order to determine if it's using plain HTTP or not. If so, perform the redirection.

Finally, the `All` Mode, which checks both the X-Forwarded-Proto Header AND the request.TLS variable.
