---
up:
  - "[[React]]"
  - "[[Programming MOC]]"
related: 
created: 2024-05-18
tags:
---
- We will use React
- If we used HTML, CSS and JS but this called vanilla JS
	- We write code HTML and browser convert it to -> DOM (Document Object Model) tree of notes and we can change nodes with JS (make it dynamic)
	- It's more complicated so we use React
- React is divide page into components and we can use it:
	- Nav Bar (Login - signup - ..)
		- If I clicked login it will go to `/login`
	- More
- [Quick Start – React](https://react.dev/learn)

## next.js
- We will use it 
- to initilize the project with it 
  `npx create-next-app@latest`
- I faced error here so I wanted to install `npm install create-next-app@latest --save`

| Feature                       | App Router                  | Pages Router  |
| ----------------------------- | --------------------------- | ------------- |
| Routing type                  | Server-centric (Full stack) | Client-side   |
| Support for Server Components | Yes                         | No            |
| Complexity                    | More complex                | Simpler       |
| Performance                   | Better                      | Worse         |
| Flexibility                   | More flexible               | Less flexible |
