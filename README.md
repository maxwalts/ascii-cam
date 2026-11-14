# ASCII Cam

An audio-reactive ASCII webcam that runs in your browser. It cuts you out of the background, draws you in ASCII characters, and pulses along with any audio file you drop onto the page. It's built for making visuals to go with DJ mixes.

It's a single HTML file, with no install and no build step.

**[Try the live demo](https://maxwalts.github.io/ascii-cam/)**

## Example

[![Max Control — Live at Bourbon on Division (Nov 2026) [Visualizer]](https://img.youtube.com/vi/d-Z_tED9oJ0/maxresdefault.jpg)](https://www.youtube.com/watch?v=d-Z_tED9oJ0)

*Max Control live at Bourbon on Division, Chicago. This 20-minute house set was recorded with this tool. Click to watch on YouTube.*

## How it works

- **Background removal:** [MediaPipe's selfie segmentation](https://ai.google.dev/edge/mediapipe/solutions/vision/image_segmenter) runs in the browser and finds you in the webcam image, so only you show up.
- **ASCII:** each frame is shrunk to a grid, and each cell's brightness picks a character from ` .:-=+*#%@`.
- **Audio reactivity:** the Web Audio API analyses the dropped track. Kick drums brighten the image and make the grid finer, and loudness speeds up the colour cycle.
- **Colours:** cycles through a palette taken from a photo of a rave (blues, laser green, orange).
- **Recording:** saves the canvas and the track's audio to a video file you can post.

## Usage

1. Open `index.html` in Chrome (or use the live demo)
2. Click **start** and allow camera access. The microphone isn't used.
3. Drag an audio file (your mix) onto the page.

| Key   | Action                                           |
| ----- | ------------------------------------------------ |
| Space | Play / pause the track                           |
| R     | Start or stop recording (downloads the video)    |
| A     | Switch aspect ratio: 16:9, 9:16, 1:1             |
| Q     | Switch output resolution: 1080p / 4K             |
| H     | Hide or show the help text (it's never recorded) |

Notes:
- Recording runs in real time, so keep the tab visible while it records. Chrome pauses background tabs.
- Recordings are 60fps. For YouTube, record in 4K (press Q) even if most people watch in 1080p: YouTube gives 4K uploads more bitrate, which keeps the characters sharp. Close other apps so the frame rate stays steady.
- The first load needs internet to fetch the segmentation model.

## Tuning

All the settings are at the top of the `<script>` in `index.html`:

| Setting         | What it does                                                               |
| --------------- | -------------------------------------------------------------------------- |
| `PALETTE`       | Colours to cycle through (RGB). Repeat a colour to make it last longer.    |
| `ROWS`          | Rows of text. Lower gives bigger characters and a less recognisable image. |
| `CHARS`         | Character ramp, from dark to bright                                        |
| `MUSIC_BOOST`   | How much loudness brightens the characters                                 |
| `KICK_BOOST`    | Extra brightness flash on each kick                                        |
| `CUTOFF`        | Person-mask threshold. Raise it if the background bleeds in.               |
| `MOTION_CUTOFF` | Lower threshold for moving areas. Lower it if fast hands get clipped.      |
| `MOTION_AMOUNT` | How much change counts as movement                                         |
| `FPS`           | Recording frame rate                                                       |
| `BITRATE`       | Recording bitrate per resolution (1080p / 4K)                              |

## License

MIT
