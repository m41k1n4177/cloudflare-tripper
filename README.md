# Go CloudFlare ByPass

[![Coverage Status](https://coveralls.io/repos/github/DaRealFreak/cloudflare-bp-go/badge.svg?branch=master)](https://coveralls.io/github/DaRealFreak/cloudflare-bp-go?branch=master)
![GitHub](https://img.shields.io/github/license/DaRealFreak/cloudflare-bp-go)
[![Go Report Card](https://goreportcard.com/badge/github.com/DaRealFreak/cloudflare-bp-go)](https://goreportcard.com/report/github.com/DaRealFreak/cloudflare-bp-go)

The Go CloudFlare ByPass is a small round tripper that prevents triggering CloudFlare's "attention required" status for HTTP requests. It achieves this by adding the required/validated headers on requests and updating the client TLS configuration to pass the CloudFlare validation.

It's important to note that this package is NOT intended to solve challenges provided by CloudFlare. Instead, it's designed to prevent CloudFlare from directly displaying a challenge on the first request.




## Dependencies
- [eddycjy/fake-useragent](https://github.com/EDDYCJY/fake-useragent) - used for setting a believable request user agent. Although CloudFlare is relatively forgiving with user agents, it's good to add some variety for the long term.

## Usage
You can add the round tripper as you would any other round tripper:
```go
client := &http.Client{}
client.Transport = cloudflarebp.AddCloudFlareByPass(client.Transport)
```

### NB!

Using the http.DefaultTransport will currently fail. Instead, use nil or empty &http.Transport.
