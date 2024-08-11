---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-07-25
Link: https://intelegain-technologies.medium.com/what-are-web-frameworks-and-why-you-need-them-c4e8806bd0fb
---

- a software framework that is designed to support the development of web applications including web services, web resources and web APIs
- بتبقا عبارة عن Software بيوفرلك طريقة عشان تـ Create and run الـ Web application بتاعك
- فالأول كنت بتقدر تعدل الحاجات دي بس دلوقتي بتختار الأنسب على حسب الـ Project بتاعك

## CMS vs Framework
CMS (Content Management System)
- لما الشخص بيبدأ يعمل موقع جديد بيبقا محتاج Tools ففيه ناس بتبدأ From Scratch وفيه ناس معندهاش خلفية فمش بتحب تعمل كدا أو معندهاش خبرة تعمل كدا
- الـ CMS بيشيل الضغط بتاع الخبرة دا، على عكس الـ Framework اللي بتوفر features عشان تعمل custom application 
- The main difference between the two is the approach, like for instance, navigating your system through a command line (framework) vs an explorer (CMS).
- عن طريق الـ CMS بيبقا عندك pre-set features وبيبقا ليك Theme معين للسايت وتقدر تضيفله ميزات جديدة ودا هيزود التعقيد بس تقدر تظبط احتياجاتك 
- باستخدام الـ Framework بتبني كل حاجة From scratch بس تقدر تعمل Unique features
- Frameworks are highly customizable, whereas CMS typically have limitations. 
- Plus, since web frameworks are usually a set of libraries and tools that help in building web apps, they require higher programming knowledge and skills.
- With CMS you don’t need to have programming skills, this is true, but that is only if you are maintaining a website that already exists. To set up a web app through a CMS you will at least need to know how to work with a server and how to read and edit pieces of code.

## Types of Web frameworks
we have two functions of frameworks — 
a) the one to work on the server side, that helps to set up app logic on the server (backend)
b) to work on the client-side (front end).

![[Pasted image 20240725075646.png]]

### 1. Server-side Frameworks
Server-side frameworks handle [[HTTP]] requests, database control and management [[Database Management System (DBMS)|Using DBMS]], URL mapping, etc.

- .NET (C#)
- Django (Python)
- Ruby on Rails (Ruby)
- Express (JavaScript/Node.JS)
- Symfony (PHP)

### 2. Client-side Frameworks
Client-side frameworks don’t take care of the business logic like the server-side ones. They function inside the browser. 
Therefore, you can enhance and implement new user interfaces. A number of animated features can be created with frontend and single page applications

- **Angular**
- **Ember.JS**
- **Vue.JS**
- **React.JS** [[React]]

## Web application framework- Architecture
Most of the web frameworks depend on the MVC (Model-View-Controller) architecture. 
The reason why this pattern is preferred lies in its rational design that **separates the app logic from the interface**
It forms تمثل the three essential parts that are represented in the architecture’s name — MVC (Model-View-Controller).

![[Pasted image 20240725081051.png]]

### Model

The Model comprises of all the data, business logic layers, its guidelines and functions. 
The Model, upon getting user input data from the Controller, tells the way an updated interface should be displayed directly to the View.

### View

The View is for the graphical representation of the data like graph or charts etc. 
It is the apps’ front-end. 
The View gets the user input and communicates the same to the Controller for examination and then update and reconstructs itself according to the Model’s instructions, or the Controller’s in case the modification requirement is minimum.

### Controller

The Controller translates the input data into the scope of commands of the previous ones. 
It is the midway between the Model and the View. 
It gets the user input from the View; after processing it, the Controller notifies the Model (or View) of the changes required.

The talking point about many discussions regarding the Controller is that it **isn’t always essential** (giving more importance to the separation of logic from the interface). 
Assigning input processing, however, to either Model or View messes up the MVC’s traditional mantra of ‘Separated Presentation’-where tasks are separated on type-basis.
For the project to remain transparent, adaptable and maintainable, each component in the MVC must be responsible for a sole line of tasks.