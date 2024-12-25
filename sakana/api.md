---
title: API | Sakana Docs
description: Documentation of the sakana api
---

When you add Sakana to your website you can use the api to load games, change settings and other.

> [!WARNING]
> Sakana is in a development state, this means the api changes frequently and that the docs *might* be outdated.

# Basic File loading
```js
import { Sakana } from 'path/to/sakana/core/index.js'

let emulator = new Sakana('div id');

emulator.load(game file, key file);
```
Note that the files passed must be from a input.

# Full api
- Sakana [Class]:\
When initiated pass a string with the id of a div where.\
This will return a emulator object with functions and properties.
- Emulator [Object]:\
This includes everything not game specific.\
Properties:
  - root - div id
  - canvas - canvas
  - ctx - canvas ctx
  - width - emulator screen width [Editable]
  - height - emulator screen height [Editable]
  - game - Game object, game settings and more
  - load(file, keys) - Loads a file with keys to be emulated
- Game [Object]:\
This includes game specific things.\
Properties:
  - framerate - Game framerate
  - data - Game data (files and other)
  - paused - Is it paused? [Editable]
  - loading - Is it in loading state?
  - pause() - Pauses playback
  - resume() - Resumes playback
  - fullscreen() - Makes game fullscreen