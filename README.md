# egamebook.com site [![Build Status](https://api.cirrus-ci.com/github/filiph/egamebook_site.svg)](https://cirrus-ci.com/github/filiph/egamebook_site)

Use `make` to build, serve and deploy. For example:

* `$ make install` to install everything necessary
* `$ make build` to build the site from source
* `$ make serve` to develop the site on `localhost:3000` with a fast edit-refresh cycle, using
  [BrowserSync](https://www.browsersync.io)
* `$ make deploy` to upload to Firebase
* `$ make clean` to clean up all generated files, useful for a clean build

## Video on site

The homepage has a video screencast of the game in action. To get it, record a device screen with the correct screen ratio (480 x 984). Then compress the video using something like [VideoSmaller](http://www.videosmaller.com/) with width of 480 pixels. (The site has better results than whichever command line tool and preset I've tried so far.)

## Before Deploying

### Invalidate cached assets

Before deploying any changes to CSS, images or other media linked in HTML or CSS, update query
string in all requests for such assets. Make sure all requests for a file use the same query
string, eg.:

```html
<link rel="preload" href="/css/main.min.css?v=2019021201" as="style" />
<!-- … -->
<link rel="stylesheet" href="/css/main.min.css?v=2019021201" />
```

This will force browsers to download the assets even if they had been cached before (may not work
for proxy servers that strip query strings).

### Check links

Always check that links work before deployment. Recommended approach:

#### One-time install 

1. Install [Dart SDK](https://www.dartlang.org/tools/sdk#install), 
   and make sure it's in `$PATH`
2. Install `linkcheck` via `pub global activate linkcheck`

#### Check

1. Start the local server via `make serve`
2. Run `linkcheck` via `linkcheck :5000` (this checks `localhost:5000`)
3. (Optionally) Check external links with `linkcheck :5000 -e`
