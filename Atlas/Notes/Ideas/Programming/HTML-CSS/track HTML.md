---
up:
  - "[[HTML]]"
related: 
created: 2024-06-22
---

The `<track>` element defines text tracks, such as subtitles or captions, for `<audio>` and `<video>` elements. 
This text should be visible as the related media source it playing, and are formatted in the WebVTT (.vtt) format.

```html
<video>
  <source src="common_html_elements.mp4" type="video/mp4">
  <track src="english_subtitles.vtt" kind="subtitles" srclang="en" label="English">
  <track src="spanish_subtitles.vtt" kind="subtitles" srclang="es" label="Spanish">
</video>
```