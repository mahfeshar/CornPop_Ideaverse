---
up:
  - "[[HTML]]"
related: 
created: 2024-06-22
---

`<audio>`: is used to embed sound content, such as music or podcasts. It contains one or more `<source>` tags with different audio sources
(e.g. MP3, WAV), so the browser can select the first supported source to play.

If a browser does not support the audio formats provided, the browser will instead display any text within the `<audio>` element.

```html
<audio>
	<source src="soundtrack.mp3" type="audio/mpeg">
	<source src="soundtrack.ogg" type="audio/ogg">
	Your browser does not support the audio formats provided.
</audio>
```