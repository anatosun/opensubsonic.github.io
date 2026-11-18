---
title: "getWaveform"
linkTitle: "getWaveform [OS]"
OpenSubsonic:
  - Extension
categories:
  - Media retrieval
description: >
  Returns the loudness envelope of a song.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songWaveform` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

`http://your-server/rest/getWaveform`

Returns the loudness envelope of a song: the song is split into `samples` slices of equal duration, and each slice gets one loudness value on a linear `0`–`255` scale, where `255` is the loudest slice of the song. Clients can use it to draw a waveform, for example behind the seek bar.

How loudness is measured is up to the server. RMS amplitude is recommended over peak amplitude, because mastered music sits near full scale almost everywhere and a peak envelope looks flat.

Servers may compute waveforms on demand, so the first request for a song can take longer than later ones. A server that advertises the extension but cannot produce a waveform for a song (for example because waveforms are turned off) returns a regular [`error`](../../responses/error).

### Parameters

| Parameter | Req. | OpenS. | Default | Comment |
| --- | --- | --- | --- | --- |
| `id` | **Yes** | **Yes** | | The ID of the song. |
| `samples` | No | **Yes** | `500` | The number of loudness values to return. Must be a positive integer. Servers may cap it to their maximum resolution, in which case they return fewer values than requested. |

### Example

{{< alert color="primary" >}} `http://your-server/rest/getWaveform.view?id=300000060&samples=8&u=demo&p=demo&v=1.16.1&c=AwesomeClientName&f=json` {{< /alert >}}

### Result

A [`subsonic-response`](../../responses/subsonic-response) element with a nested [`waveform`](../../responses/waveform) element on success.

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
  "subsonic-response": {
    "status": "ok",
    "version": "1.16.1",
    "type": "AwesomeServerName",
    "serverVersion": "0.1.3 (tag)",
    "openSubsonic": true,
    "waveform": {
      "id": "300000060",
      "duration": 304.5,
      "samples": 8,
      "peaks": [12, 96, 180, 255, 231, 160, 88, 5]
    }
  }
}
{{< /tab >}}
{{< tab header="Subsonic" lang="json" >}}
Does not exist.
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `waveform` | [`waveform`](../../responses/waveform) | **Yes** | **Yes** | The loudness envelope of the song. |
