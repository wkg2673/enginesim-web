# Engine Simulator - Web Build

A browser version of Engine Simulator, compiled to WebAssembly from the
open-source v0.1.12 source (fork: `bobsayshilol/engine-sim`, branch
`wasm-build`). Loads the included Subaru EJ25 engine (`atg-video-2`).

<img width="2559" height="1439" alt="image" src="https://github.com/user-attachments/assets/2ae4fb1c-ec57-4c2e-9b24-fb6449333d55" />


## How to run

Serve this directory over HTTP, then open `index.html`:

```
python -m http.server 8000
```

Then browse to `http://localhost:8000/index.html`.

Or go to [to8-engine-sim.netlify.app](https://to8-engine-sim.netlify.app/) for the Netlify version i host.

## Controls

- Throttle: `Q` / `W` / `E` / `R`
- Brake : `.` 
- Shift : `UP` / `DOWN` (arrow keys)
- Clutch: `Shift`
- Slow-Mo: `1 - 5`
- Fullscreen: `F`

## Loading your own engine file

Click **Load Engine (.mr)** in the top-right corner and pick a `.mr` engine
script. If the script compiles, it replaces the current engine and the file
bar shows `Loaded: <name>`. If it fails (e.g. a rotary/Wankel `.mr` file that
needs native Wankel nodes), the file bar shows `Failed to compile scripts -
see browser console for details`, the compile errors are printed to the
browser console, and the currently running engine is left untouched.

Engine files must use the modern format that ends with a `public node main`
which calls `set_engine(...)`; anything else will be rejected with a warning.

## Notes

- The audio may sometimes be chopped and if you switch tabs it repeatedly
  plays the audio.
- The build is a single self-contained `index.html` (HTML + JS + WASM +
  embedded data). No other files are required to serve it.
- The 4 messages like `Error @ yds_opengl_device.cpp:875 - 1` and
  `Error @ yds_interchange_file_0_1.cpp` in the console are benign
  (WebGL / assets.dia interchange) and do not affect functionality.
- Your locally installed v0.1.14a program data (incl. rotary/Wankel engines)
  is NOT used here: the v0.1.14a source is closed-source and its scripts
  require native Wankel nodes that no open-source engine-sim build provides.
  This web build therefore uses the v0.1.12 open-source data (piston engines
  only).

## Thanks
Thanks for AngeTheGreat who made the original engine-sim, which you can check out here: [engine-sim by Ange Yaghi](https://github.com/ange-yaghi/engine-sim)
