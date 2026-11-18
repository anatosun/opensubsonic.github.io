---
title: "Song waveform"
linkTitle: "Song waveform"
OpenSubsonic:
  - Extension
description: >
  Retrieve a loudness envelope of a song, for example to draw a waveform seek bar.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songWaveform` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

## Version 1

This extension requires the following endpoints:

- [`getWaveform`](../../endpoints/getwaveform): Fetch the loudness envelope of a song by id

The endpoint returns a [`waveform`](../../responses/waveform) element, which holds one loudness value per equal-length slice of the song.
