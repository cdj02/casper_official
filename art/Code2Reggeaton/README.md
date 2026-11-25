# Code2Reggaeton – web player

Hear a code smell. Flip between a clean and a smelly version of the same program, listen to the
reggaeton beat it was turned into, and read the source code side by side.

Plain HTML/CSS/JS. No build step, no framework, no internet needed.

## Run it

Browsers refuse to load audio/JSON when `index.html` is opened by double-click, so serve the folder:

    cd code2reggaeton-web
    python3 -m http.server 8000        # Windows: py -m http.server 8000

then open http://localhost:8000 . Press F for fullscreen.

## Put in your own data

The folder ships with **demo placeholder** data (rough stand-ins, not your real engine output).
Delete the contents of `data/` and drop in yours:

    data/
      sonification_data.json    <- the same file the SuperCollider workbench reads
      audio/pair_01_clean.wav     pair_01_smelly.wav  ...
      code/pair_01_clean.java     pair_01_smelly.java ...

The file names are built from the pair id in the JSON (`<pairId>_<clean|smelly>`). If your files are named
differently, change the two lines at the top of the script in `index.html`:

    audioPath: (id, state) => `data/audio/${id}_${state}.wav`,
    codePath:  (id, state) => `data/code/${id}_${state}.java`,

or set explicit paths per entry in the JSON, next to `"metrics"`:

    "smelly": { "metrics": {...}, "audio": "any/path.wav", "code": "any/path.java" }

Sounds are looped seamlessly, so WAVs that are a whole number of bars long loop best.

## Keys

| Key | Action |
|---|---|
| Space | switch clean / smelly (restarts on the first beat) |
| Left / Right | previous / next pair |
| 1 - 4 | jump to a smell category |
| Up / Down (hold to glide), PgUp / PgDn, Home / End | scroll the code |
| P | pause / play |
| + / - | code text size |
| F | fullscreen |

## Sharing it

It is a static site, so any static host works. Easiest: drag the whole folder onto https://app.netlify.com/drop
or push it to a GitHub repo and enable GitHub Pages. You get a link anyone can open.
