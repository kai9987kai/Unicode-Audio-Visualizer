# Unicode Audio Visualizer — Advanced Studio

A modern, browser-based audio visualizer that turns music, sound files, or live microphone input into animated Unicode art and reactive canvas effects. This project began as a simple frequency-to-Unicode visualizer and has been expanded into a full single-file audio visualization studio with multiple display modes, live audio metrics, export tools, presets, and advanced Web Audio controls.

The app runs entirely in the browser with no build step and no external libraries.

---

## Overview

**Unicode Audio Visualizer — Advanced Studio** lets you upload an audio file or use your microphone, then converts the live audio signal into animated Unicode output. It keeps the original core idea — mapping analyser frequency data into Unicode characters — while adding a professional interface, multiple visualization engines, beat detection, canvas rendering, snapshots, fullscreen mode, keyboard shortcuts, and persistent settings.

The project is ideal for:

* Creative coding experiments
* Audio-reactive art
* Browser-based visual demos
* Unicode/ASCII art generation
* Web Audio API learning
* Music visualization prototypes
* Live microphone visual feedback

---

## Features

### Original Features Preserved

* Upload an audio file from your device
* Play uploaded audio in the browser
* Analyze audio with the Web Audio API
* Convert frequency data into Unicode characters
* Display a live text-based visualizer
* Render continuously with `requestAnimationFrame`

---

### New Advanced Features

#### Audio Sources

* Audio file upload
* Drag-and-drop audio loading
* Live microphone input mode
* Safe cleanup when switching sources
* Automatic object URL cleanup
* Browser-native audio controls
* Local-only processing; audio is not uploaded anywhere

#### Visualization Modes

The app includes several real-time visual styles:

1. **Unicode Bars**
   Classic frequency bars rendered as Unicode characters.

2. **Unicode Wave**
   Oscilloscope-style waveform rendered as text.

3. **Glyph Matrix**
   A reactive field of symbols, blocks, dots, and animated characters.

4. **Radial Spectrum**
   Circular spectrum visualization with canvas glow effects and Unicode overlay.

5. **Spectrogram Trail**
   A scrolling frequency history view that creates a heatmap-like trail.

---

### Unicode Palettes

Choose from multiple character sets:

* Blocks: `█▇▆▅▄▃▂▁`
* Braille-inspired glyphs
* Shade blocks: `░▒▓█`
* Spark symbols
* Wave bars
* ASCII: ` .:-=+*#%@`

These palettes let the same audio produce very different text-art styles.

---

### Live Controls

The upgraded interface includes real-time controls for:

* FFT size
* Smoothing amount
* Output gain
* Unicode density
* Beat detection sensitivity
* Mirror mode
* Canvas glow
* Peak hold
* Auto rotation
* Theme switching
* Visualization mode switching
* Character palette switching

All controls update live while audio is playing.

---

### Beat Detection and Metrics

The app computes and displays live audio metrics:

* RMS volume
* Peak frequency band
* Beat state
* Frames per second

Beat detection is based on low-frequency energy compared against a rolling average. This allows the interface to react to kicks, bass hits, and sudden dynamic changes.

---

### Presets

Four built-in presets make it easy to change the visual style instantly:

| Preset   | Description                          |
| -------- | ------------------------------------ |
| Calm     | Smooth waveform-focused visual style |
| Club     | High-energy radial spectrum mode     |
| Terminal | ASCII/matrix-inspired text output    |
| Cinema   | Large spectrogram-style visual mode  |

The most recently used preset is saved to `localStorage`.

---

### Export Tools

The visualizer includes creative export options:

* Save the canvas visual as a PNG image
* Copy the current Unicode frame to the clipboard
* Export the current Unicode frame as a `.txt` file
* Use fullscreen mode for presentations or live display

---

### Keyboard Shortcuts

| Key     | Action                       |
| ------- | ---------------------------- |
| `Space` | Play or pause uploaded audio |
| `M`     | Cycle visualization mode     |
| `T`     | Toggle light/dark theme      |
| `F`     | Toggle fullscreen            |

---

## Demo Workflow

1. Open the HTML file in a modern browser.
2. Drop an audio file onto the upload zone, or click the upload area and choose a file.
3. Press play if the file does not automatically start.
4. Try different visualizer modes.
5. Adjust density, FFT size, smoothing, and beat sensitivity.
6. Save a PNG snapshot or export the current Unicode frame.
7. Switch to microphone mode for live audio-reactive visuals.

---

## Installation

No installation is required.

Download or clone the project, then open the HTML file directly in a browser:

```bash
open unicode_audio_visualizer_advanced.html
```

Or serve it locally with a simple development server:

```bash
python -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

Using a local server is recommended for the best browser compatibility, especially when using microphone permissions.

---

## File Structure

This project is designed as a single-file application:

```text
unicode_audio_visualizer_advanced.html
```

The file contains:

```text
HTML   — interface structure
CSS    — responsive glassmorphism UI and visual styling
JS     — Web Audio setup, analyser logic, Unicode rendering, canvas effects, controls, presets, and export tools
```

No bundler, package manager, framework, or dependency installation is required.

---

## How It Works

### 1. Audio Input

The app accepts either:

* A local audio file through an `<input type="file">`
* A dropped audio file
* A microphone stream through `navigator.mediaDevices.getUserMedia`

For file playback, the app creates an `Audio` element and connects it to a Web Audio graph.

---

### 2. Web Audio Graph

The audio graph follows this structure:

```text
Audio Source / Microphone
        ↓
AnalyserNode
        ↓
GainNode
        ↓
AudioContext Destination
```

The `AnalyserNode` provides:

* Frequency data using `getByteFrequencyData()`
* Time-domain waveform data using `getByteTimeDomainData()`

---

### 3. Unicode Rendering

The original idea is preserved and improved:

```js
const value = dataArray[i];
const character = String.fromCharCode(9608 + Math.floor(value / 25));
```

The advanced version replaces the fixed character conversion with selectable palettes and multiple rendering functions. Frequency and waveform data are sampled, normalized, and mapped into Unicode characters based on the selected mode.

---

### 4. Canvas Rendering

In addition to text output, the app renders a reactive canvas layer. Depending on the selected mode, the canvas may draw:

* Frequency bars
* Waveform lines
* Radial spectrum rays
* Spectrogram trails
* Beat-reactive particles
* Glow effects
* Peak hold markers

The Unicode output is layered above the canvas for a hybrid text-and-graphics effect.

---

### 5. Beat Detection

The app measures average energy in the low-frequency range and compares it against a rolling average. When low-frequency energy rises above the threshold, the interface treats it as a beat.

This beat signal drives:

* Glow intensity
* Radial pulse size
* Particle size
* Beat status metric
* Matrix glyph flashes

---

## Browser Support

Recommended browsers:

* Chrome / Chromium
* Edge
* Firefox
* Safari

Required browser APIs:

* Web Audio API
* Canvas API
* File API
* Clipboard API for copy support
* Fullscreen API for fullscreen mode
* MediaDevices API for microphone mode

Microphone mode requires browser permission and may work best when served from `localhost` or HTTPS.

---

## Privacy

This app runs fully in the browser.

* Uploaded audio files stay on your device.
* Microphone audio is processed locally.
* No audio is sent to a server.
* No account is required.
* No external tracking libraries are used.
* Settings are stored locally with `localStorage`.

---

## Accessibility Notes

The interface includes:

* Clear labels for controls
* Keyboard shortcuts
* Native audio controls
* Text-based visual output
* Light and dark themes
* Responsive layout for smaller screens

Because the visualizer uses rapid animation and flashing effects, users sensitive to motion or flashing should reduce glow, choose the Calm preset, or avoid fullscreen high-intensity modes.

---

## Customization

### Add a New Unicode Palette

Add another entry to the `charsets` object:

```js
const charsets = {
  custom: ' .oO@#█'
};
```

Then add a matching option to the palette dropdown:

```html
<option value="custom">Custom .oO@#█</option>
```

---

### Add a New Preset

Add a preset inside the `presets` object:

```js
myPreset: {
  mode: 'matrix',
  charset: 'spark',
  smoothing: 0.75,
  density: 100,
  sensitivity: 1.25,
  glow: true,
  mirror: true,
  gain: 1.0
}
```

Then create a button that calls:

```js
applyPreset('myPreset');
```

---

### Add a New Visual Mode

To add another mode:

1. Add a new `<option>` in the mode dropdown.
2. Create a new Unicode rendering function.
3. Add the mode to `updateUnicode()`.
4. Add optional canvas behavior inside `drawCanvas()`.

---

## Suggested Future Improvements

Potential next upgrades:

* Audio recording of visualizer sessions
* GIF or WebM export
* MIDI controller support
* Multi-track comparison mode
* Audio-reactive color themes
* Lyric or subtitle overlay support
* More Unicode art modes
* 3D WebGL visualizer layer
* Preset import/export
* BPM estimation
* Frequency band solo/mute controls
* Visual timeline scrubber
* Project save/load system
* Mobile gesture controls
* PWA offline installation

---

## Troubleshooting

### Audio does not play

Some browsers block autoplay until the user interacts with the page. Click the play button or the native audio controls.

### Microphone does not work

Check that:

* The browser has microphone permission
* The page is served from HTTPS or `localhost`
* Another app is not blocking the microphone

### Visualizer is slow

Try:

* Lowering Unicode density
* Lowering FFT size
* Turning off glow
* Using Calm or Terminal preset
* Closing other heavy browser tabs

### Clipboard copy fails

Clipboard access may require a secure context or user interaction. Use the TXT export button instead.

---

## Technical Highlights

* Single-file HTML/CSS/JavaScript app
* No external dependencies
* Uses `AudioContext`, `AnalyserNode`, and `GainNode`
* Uses `requestAnimationFrame` for real-time rendering
* Uses `Uint8Array` buffers for frequency and waveform data
* Uses local object URLs for audio playback
* Uses `localStorage` for theme and preset persistence
* Uses Canvas 2D for reactive visual effects
* Uses Unicode text rendering for the main visual identity

---

## Project Goals

The goal of this project is to explore how far a simple browser audio visualizer can be pushed while remaining lightweight, portable, and easy to understand.

The upgraded version focuses on:

* Keeping the original Unicode visualizer concept
* Making the interface more polished and interactive
* Adding creative audio-reactive modes
* Improving browser safety and cleanup
* Supporting both files and live microphone input
* Providing exportable visual output
* Remaining dependency-free and beginner-friendly

---

## License

You can use this project as a starting point for your own creative coding, audio visualization, or browser-based media experiments. Add your preferred license file if you plan to publish the project publicly.

A common choice for open-source browser demos is the MIT License.

---

## Credits

Built with standard browser technologies:

* HTML
* CSS
* JavaScript
* Web Audio API
* Canvas API
* Unicode text rendering

Inspired by classic audio spectrum analyzers, terminal art, ASCII visualizers, oscilloscope displays, and creative coding experiments.
