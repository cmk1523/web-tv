# web-tv

A single-page viewer for four live HLS (`.m3u8`) streams. Open `quad.html` in a browser to watch them in a quad, stacked, or side-by-side layout, with world clocks across the top.

## Run

HLS playback needs a web origin. Serving the folder locally avoids `file://` restrictions:

```bash
python -m http.server 8000
```

Then open [http://localhost:8000/quad.html](http://localhost:8000/quad.html).

Playback uses [hls.js](https://github.com/video-dev/hls.js) from jsDelivr. Safari plays HLS natively and does not need that script. Each stream URL must allow cross-origin requests from the page, or the browser will refuse to load it.

## Configure streams

Edit the `streams` array near the top of the script in `quad.html`. The page fills the four video slots in order:

```js
const streams = [
    { title: 'CBS Sports', url: 'https://example.com/index.m3u8' },
    { title: 'FOX LiveNOW', url: 'https://example.com/live.m3u8' },
    { title: 'NBC News', url: 'https://example.com/master.m3u8' },
    { title: 'CBS News', url: 'https://example.com/master.m3u8' }
];
```

Hover a title to reveal a link that opens that stream’s playlist.

## Controls

The menu on the clock bar remembers these choices in `localStorage`:

- **Layout** — Quad (2×2), Vertical (four rows), or Horizontal (four columns)
- **Titles** — drawn over the video, or on a bar above it
- **Text color** — red, green, blue, orange, or white
- **Timezone bar** — show or hide the clocks (Los Angeles, New York, London, Tokyo, Sydney, 24-hour)

Videos start muted so autoplay is allowed. Use each player’s controls to unmute.
