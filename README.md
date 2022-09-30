# Videos inserted via Unpoly do not show up in Safari

This repository is the simplest project necessary to reproduce a bug that happens for videos inserted via Unpoly in Safari.

When navigating with Unpoly (e.g. using links with the attribute `up-target="body"`), videos do not show up at all in macOS Safari.

## Expected behavior (Firefox)

I can click Unpoly links that lead to pages with videos and the videos are always visible, autoplaying, and have controls.

![](./firefox.gif)

## Actual behavior (Safari)

When I click Unpoly links that lead to pages with videos, the videos do not load. I have to reload the page to see the videos.

![](./safari.gif)

## Workaround

This problem can be "fixed" for autoplaying videos by calling their `play` (or `load`) method. This loads and plays the video. But this only works for autoplaying videos without controls - for videos with controls, the controls do not show up when this "fix" is applied. The controls also do not show up whe right-clicking on the video and choosing "show/hide controls".

```js
up.compiler('video[autoplay]', async function (video) {
  try {
    await video.play()
  } catch (err) {
    // do nothing
  }
})
```

## Setup

You will need a web server that can serve static files from this directory. 

For example `adsf` (A Dead Simple Fileserver) which is a Ruby gem. I can be installed and started with:

```
$ gem install adsf
$ gem install puma
$ adsf -p 5555
```

Visit `localhost:5555/page1.html` to see the bug in action.
