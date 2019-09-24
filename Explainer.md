WebMediaContainers
--

API that allows web applications to write, read, edit, extract, and merge audio and video to and from a media container.

`MediaRecorder` provides the capability to write real-time captured audio and video to a media container.

However `MediaRecorder` does not provide a means to write non-real-time audio and video to a media container.

[WebCodecs](https://discourse.wicg.io/t/webcodecs-proposal/3662) proposal while having similar use cases, including

> - Media file editing and transcoding

is not presently focused on development and standardization of writing the media output by that API to a media container [API for containers? #24](https://github.com/WICG/web-codecs/issues/24).

This propsal is very simple: an API focused on writing, reading, editing, extracting, muxing, merging and audio, video, subtitles, captions to and from a media container, both in real-time and post-production. 

The proposal intends to specify WebMediaContainers API separate but concurrent to WebCodecs API, for the purpose of the two proposals to be developed at approximately the same rate, for the goal of interopability with while simultaneously capable of interaction with audio, video, text tracks APIs other than WebCodecs.

```
    let videoWriter = new WebMediaContainer({videoCodec:"WebM", audioCodec:"Opus", ...videoWriterSettings});
    videoWriter.addVideoFrame(
      videoFrame /* WebP, PNG, etc. as Blob, ArrayBuffer, data URI, ImageBitmap, ImageData, canvas */, frameDuration, width, height, /* WebVTT, ...frameSettings */
    );
    videoWriter.addAudioFrame(
       audioFrame /* AudioBuffer, Float32Array, Blob, ArrayBuffer, data URI, other... */, sampleRate, numberOfChannels, frameDuration
    );
    await videoWriter.compile(); // Blob
```

Expose the media encoders, muxers, and containers writers that the browsers already have in source code directly to the developer. 

Again, the concept is very simple. Browsers that have implemented `MediaRecorder` already write data to a container, currently WebM or Matroska. 
The developer should be able to use that internal code in JavaScript. Whether the input be static files or live media.
