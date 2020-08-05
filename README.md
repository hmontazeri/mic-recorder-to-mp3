# ~~Microphone~~ Stream Recorder to Mp3

This is a fork of https://github.com/closeio/mic-recorder-to-mp3

Record your ~~microphone~~ media stream object audio input and get an `audio/mp3` file in the end.

# Install

## Yarn

```bash
yarn add stream-recorder-to-mp3
```

## npm

```bash
npm install stream-recorder-to-mp3
```

# Development

- Watch for changes:

```bash
npm run watch
```

- Regular build:

```bash
npm run build
```

# How to use

```js
const StreamRecorder = require("stream-recorder-to-mp3");

// New instance
const recorder = new StreamRecorder({
  bitRate: 128,
  stream: myMediaStreamObject,
});

// Start recording. Browser will request permission to use your microphone.
recorder
  .start()
  .then(() => {
    // something else
  })
  .catch((e) => {
    console.error(e);
  });

// Once you are done singing your best song, stop and get the mp3.
recorder
  .stop()
  .getMp3()
  .then(([buffer, blob]) => {
    // do what ever you want with buffer and blob
    // Example: Create a mp3 file and play
    const file = new File(buffer, "me-at-thevoice.mp3", {
      type: blob.type,
      lastModified: Date.now(),
    });

    const player = new Audio(URL.createObjectURL(file));
    player.play();
  })
  .catch((e) => {
    alert("We could not retrieve your message");
    console.log(e);
  });
```

## Lamejs Notice

This library uses lamejs as a direct dependency. We build our releases with [lamejs](https://github.com/zhuker/lamejs/) built-in, so you don't need to add another dependency.

Thanks to **@zhuker** for writing the lamejs library.

# License

MIT
