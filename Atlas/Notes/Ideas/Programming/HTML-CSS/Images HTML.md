---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---
`<img />` We will use this to add images but this is special one because *It doesn't have close tag* 
So we add / before the end of tag.

It's a [[Self-Closing Elements HTML]]


```html
<img
      src="post-img.jpg"
      alt="HTML code on a screen"
      width="500"
      height="200"
    />
```
### Attributes
> `img` has a lot of [[Attributes HTML]]


`src="name_of_the_image"` : the source for the image

`alt=""`: Alternative text, describe what the image is about.

This is important for:
- It will allow search engines to know what is in the image
- we can allow blind people to use a website
- If image cannot be found, it will appear

`width="500"` 
`height="200"`
If you add one attribute like width or height, it will automatically also maintains the aspect ratio of the image
