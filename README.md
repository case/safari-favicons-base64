## Background

Data URI base64 favicons appear to work in Chrome and Firefox, but not Safari for some reason.

[The Safari docs](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html) say to add the following to the site `<head>`:

`<link rel="apple-touch-icon" href="/custom_icon.png">`

…or put an `apple-touch-icon.png` image file at the site root.

Stack Overflow [suggests](https://stackoverflow.com/a/5199989/890466) this should work in Safari, but I'm not seeing it work in Safari 15.3 in macOS Monterey 12.2.1. This post is from 2011, so maybe something changed or broke since then?

I couldn't find anything relevant in the [WebKit bug tracker](https://bugs.webkit.org/buglist.cgi?quicksearch=favicon) either, but perhaps I missed it?

## Local dev

Launch a local web server from this directory, for example:

`$ python3 -m http.server` -> visit `http://localhost:8000` in Chrome, Firefox, and Safari.

**To see the issue:** In `index.html`, try commenting out `L8`, and uncommenting `L14`.

Safari appears to use the same favicon for all `localhost` ports, so we need to [delete its favicon cache](https://www.idownloadblog.com/2020/09/08/refresh-favicons-in-safari-mac/) when testing:

1. Quit Safari.
2. Go to `~/Library/Safari/Favicon Cache/` and delete everything in there.
3. Re-launch Safari.

`¯\_(ツ)_/¯`

## Updates

- WebKit bug filed here: https://bugs.webkit.org/show_bug.cgi?id=236616
- Twitter thread here: https://twitter.com/case/status/1493328641580621824?s=21
