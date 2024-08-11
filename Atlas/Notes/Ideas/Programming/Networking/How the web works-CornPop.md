---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-10
Link: https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works
---
## Clients and servers
![[Pasted image 20240710125143.png]]
- Clients are ==the typical web user's internet-connected devices== (for example, your computer connected to your Wi-Fi, or your phone connected to your mobile network) and ==web-accessing software available on those devices== (usually a web browser like Firefox or Chrome).
- Servers are ==computers that store webpages, sites, or apps==. 
  When a client device wants to access a webpage, a copy of the webpage is downloaded from the server onto the client machine to be displayed in the user's web browser.

We talked about it at [[Client-Server Architecture]].

## The other parts of the toolbox
عندنا حاجات تانية في النص هنعرفها دلوقتي.
لحد دلوقتي تخيل ال Web على انه طريق. في طرف من الطرفين عندك ال Client اللي ممكن نقول انه بيتك والطرف التاني فيه ال Server ممكن نقول ان دا المحل اللي هنشتري منه.

![[Pasted image 20240710125426.png]]
- **Your internet connection**: Allows you to send and receive data on the web. 
  الطريق بين البيت والمحل
- **TCP/IP**: Transmission Control Protocol and Internet Protocol are ==communication [[Protocol|protocols]] that define how data should travel across the internet==. 
  This is like the transport mechanisms that let you place an order, go to the shop, and buy your goods. 
  زي طريقة الوصول للمكان (عربية - قطر - مشي ..)
  We talked about [[What is TCP-IP]]
- **[[DNS]]**: ==[[Domain]] Name System== is like ==an address book for websites==. 
  When you type a web address in your browser, the browser looks at the DNS to find the website's IP address before it can retrieve the website. 
  The browser needs to find out ==which server the website lives on==, so it can send HTTP messages to the right place. 
  عنوان المحل اللي انت عايز توصله
- **HTTP**: Hypertext Transfer Protocol is an application [[Protocol]] that ==defines a language for clients and servers to speak to each other==. 
  اللغة اللي هتستخدمها وانت بتطلب الأوردر
- **Component files**: A website is made up of many different files, which are like the different parts of the goods you buy from the shop. These files come in two main types:
    - **Code files**: Websites are built primarily from ==HTML, CSS, and JavaScript==, though you'll meet other technologies a bit later.
    - **Assets**: This is a ==collective name for all the other stuff== that makes up a website, such as images, music, video, Word documents, and PDFs.

## So what happens, exactly?
لو مثلًا كتبت web address عندك في ال browser (انت ماشي رايح للمحل):
1. الbrowser هيروح لل DNS Server، ويدور على ال Real address of the server اللي ال website lives on
   (عرفت عنوان المحل)
2. ال Browser هيحاول يبعت HTTP request message للسيرفر، بيطلب منه يبعتله نسخة من ال Website لل Client (روحت المحل وعملت اوردر بالطلبات اللي انت محتاجها)
   كل الرسايل اللي بتتبعت دي وحتى ال data اللي بين ال Client-server بتتبعت خلال Internet connection باستخدام ال TCP/IP
3.  لو ال Server وافق على الطلب، السيرفر هيبعت لل Client رسالة "200 OK" يعني من الآخر "أكيد تقدر تشوف الموقع وخد نسخة أهو يا سيدي"، وبيبدأ يبعت ال Files بتاع الموقع لل Browser ك==series of small chunks called data packets==
   (المحل لو فيه الطلبات بتاعك، بيبدأ يدهالك وانت بتاخدها للبيت)
4. The browser assembles the small chunks into a complete web page and displays it to you (the goods arrive at your door — new shiny stuff, awesome!).

## Order in which component files are parsed
When browsers send requests to servers for HTML files, those HTML files often contain [`<link>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) elements referencing external [CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS) stylesheets and [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) elements referencing external [JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript) scripts. It's important to know the order in which those files are [parsed by the browser](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work#parsing) as the browser loads the page:

- The browser parses the HTML file first, and that leads to the browser recognizing any `<link>`-element references to external CSS stylesheets and any `<script>`-element references to scripts.
- As the browser parses the HTML, it sends requests back to the server for any CSS files it has found from `<link>` elements, and any JavaScript files it has found from `<script>` elements, and from those, then parses the CSS and JavaScript.
- The browser generates an in-memory [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) tree from the parsed HTML, generates an in-memory [CSSOM](https://developer.mozilla.org/en-US/docs/Glossary/CSSOM) structure from the parsed CSS, and [compiles and executes](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work#javascript_compilation) the parsed JavaScript.
- As the browser builds the DOM tree and applies the styles from the CSSOM tree and executes the JavaScript, a visual representation of the page is painted to the screen, and the user sees the page content and can begin to interact with it.

## DNS explained
الطريقة الأصلية اللي بعمل بيها addresses مش بتبقا زي ما بكتب جملة ولا حاجة وهيطلعلي الصفحة بتاعي.
ولكن هي عبارة عن شوية أرقام مميزة زي `192.0.2.172`
دا بنسميه [[IP Address]]، ودا بيعرفني a unique location on the web
However, it's not very easy to remember, is it? 
That's why ==the Domain Name System was invented==. (DNS)
This system uses special servers that match up a web address you type into your browser (like "mozilla.org") to the website's real (IP) address.

## Packets explained
Basically, when data is sent across the web, it is sent in ==thousands of small chunks==. 
There are multiple reasons why data is sent in small packets. They are sometimes dropped or corrupted, and it's easier to replace small chunks when this happens. 
Additionally, the packets ==can be routed along different paths==, making the exchange faster and allowing many different users to download the same website at the same time. 
If each website was sent as a ==single big chunk==, ==only one user could download it== at a time, which obviously would make the web very inefficient and not much fun to use.

