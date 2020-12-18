---
layout: post
title: "Combining audio and video files with ffmpeg"
author: "Cristina Elep"
tags: [ffmpeg]
---

A while back I was looking up how to combine an audio file (MP3) and a video file (MP4) into a single video file (MP4); I eventually found [this SuperUser StackExchange answer][ffmpeg-answer] which had exactly what I needed.

For example: Given an audio file `a.mp3` and a video file `v.mp4`, they can be combined into a single video file `out.mp4` using the following command:

```
ffmpeg -i v.mp4 -i a.mp3 -map 0:v -map 1:a -c:v copy -c:a copy out.mp4 -y
```

Here's a breakdown:
- `-i` specifies each input stream
- `-map` maps input streams to the output (0-indexed); in this case, it maps all the video streams in the first input (`v.mp4`) and all the audio streams in the second input (`a.mp3`) to the output (`out.mp4`)
- `-c:v copy -c:a copy` specifies that the streams will be copied into the output file instead of being re-encoded
- `-y` (optional) overwrites output files without asking; setting this to `-n` will cause ffmpeg to exit immediately if the output file already exists

See the [ffmpeg man page](ffmpeg-manpage) or the [ffmpeg documentation][ffmpeg-docs] for detailed descriptions of each option and how they're used.

Notes:
- I also found a [SuperUser StackExchange question about re-encoding audio][ffmpeg-reencode] from MP3 to [AAC][aac]; I haven't tried the solution in the accepted answer since I don't need to. Anyway, here's an example that converts the input audio using the built-in AAC encoder:
  ```
  ffmpeg -i input.mp3 -c:a aac output.m4a
  ```

[aac][https://en.wikipedia.org/wiki/Advanced_Audio_Coding]
[ffmpeg-answer][https://superuser.com/a/1298165]
[ffmpeg-docs][https://ffmpeg.org/ffmpeg.html]
[ffmpeg-manpage][http://manpages.org/ffmpeg]
[ffmpeg-reencode][https://superuser.com/questions/370625/ffmpeg-command-to-convert-mp3-to-aac]
[fraunhofer][https://en.wikipedia.org/wiki/Fraunhofer_FDK_AAC]
