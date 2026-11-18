---
title: "waveform"
linkTitle: "waveform [OS]"
OpenSubsonic:
  - Addition
description: >
  The loudness envelope of a song.
---

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
  "id": "300000060",
  "duration": 304.5,
  "samples": 8,
  "peaks": [12, 96, 180, 255, 231, 160, 88, 5]
}
{{< /tab >}}
{{< tab header="Subsonic" lang="json" >}}
Does not exist.
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `id` | `string` | **Yes** | **Yes** | The ID of the song. |
| `duration` | `number` | **Yes** | **Yes** | The duration of the song in seconds. |
| `samples` | `int` | **Yes** | **Yes** | The number of values in `peaks`. This can be lower than the requested number of samples. |
| `peaks` | Array of `int` | **Yes** | **Yes** | One loudness value per slice of the song, in playback order. Each slice covers `duration / samples` seconds. Values are on a linear `0`–`255` scale, where `255` is the loudest slice of the song and `0` is silence. |

In XML, each value of `peaks` is a separate `<peaks>` child element of `<waveform>`, in order.
