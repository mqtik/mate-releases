# Web Preview (/docs/features/web-preview)



Web Preview lets you view web applications running on one device from another device on your network. If your dev server is running on `localhost:3000` on your Mac, you can see it on your phone without any port forwarding or tunneling setup.

## How it works [#how-it-works]

Mate runs a reverse proxy that forwards HTTP requests from the viewing device to the target device's localhost port. The web content is rendered in an embedded browser view within Mate.

This means:

* Your dev server runs normally on localhost
* Mate proxies requests through the paired connection
* The remote device sees the page as if it were on localhost

No need to find your machine's IP address, no need to bind to `0.0.0.0`, no need for ngrok or similar tools.

## Opening a web preview [#opening-a-web-preview]

1. Click &#x2A;*+** in the tab bar
2. Select **Web Preview**
3. Enter the port number (e.g., `3000`, `8080`, `5173`)

The preview loads immediately if the server is running on that port.

## Use cases [#use-cases]

* **Mobile testing**: Preview your web app on your actual phone while developing on your desktop
* **Cross-device review**: Show a teammate the app running on your machine by having them pair their device
* **Remote monitoring**: Check on a running dev server or dashboard from your phone

<Callout type="info">
  Web Preview works for any HTTP server running on localhost — React dev servers, Next.js, Vite, Express, Django, Rails, or anything else that serves over HTTP.
</Callout>

## Live reloading [#live-reloading]

If your dev server supports hot module replacement (HMR) or live reload, it works through the preview. Changes you make in your editor trigger the same automatic refresh you would see in a local browser.

## Limitations [#limitations]

* WebSocket connections through the proxy depend on your server's WebSocket configuration
* HTTPS localhost servers may require additional setup
* The embedded browser view has standard web rendering capabilities but is not a full desktop browser
