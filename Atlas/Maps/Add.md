---
up:
  - "[[Home]]"
related:
  - "[[Relate]]"
  - "[[Communicate]]"
created: 2022-01-01
obsidianUIMode: preview
tags:
  - map/view
---
This **Add** note isn't just an inbox. It's a cooling pad 🧊.
Thoughts come in hot. But after a few days, they cool down.

> [!activity]+ ## Added Stuff
> This view looks at the 10 newest notes in your **+** folder. As you process each note: add a link, add details, move them to the best folder,  and delete everything that no longer sparks ✨. 
> 
> ``` dataview
> TABLE WITHOUT ID
>  file.link as "",
>  (date(today) - file.cday).day as "Days alive"
> 
> FROM "+" and -#x/readme 
> 
> SORT file.cday desc
> 
> LIMIT 10
> ```