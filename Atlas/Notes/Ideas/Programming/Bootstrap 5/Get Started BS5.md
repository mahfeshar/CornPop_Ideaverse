---
up:
  - "[[Bootstrap 5 MOC]]"
related: 
created: 2024-06-14
---
بتنزل ال bootstrap lib وتحطها في فولدر ال lib 
بتعمله link قبل فايل الاستايل الخاص بيك انت ودي مهمة عشان لو حبيت أعدل حاجة وبستخدم الفايل اللي امتداده `.min.css`
متعدلش في الفايل بتاع ال bootstrap 


---
## What is Bootstrap
- Bootstrap is a free front-end framework for faster and easier web development
- Bootstrap includes HTML and CSS based design templates for typography, forms, buttons, tables, navigation, modals, image carousels and many other, as well as optional JavaScript plugins
- Bootstrap also gives you the ability to easily create responsive designs

> [!radar] Responsive Web Design
> Responsive web design is about creating web sites which automatically adjust themselves to look good on all devices, from small phones to large desktops.

## Versions
Bootstrap 5 (released 2021) is the newest version of [Bootstrap](https://www.w3schools.com/bootstrap/default.asp) (released 2013); with new components, faster stylesheet and more responsiveness.

Bootstrap 5 supports the latest, stable releases of all major browsers and platforms. However, Internet Explorer 11 and down is not supported.

The main differences between Bootstrap 5 and Bootstrap 3 & 4, is that Bootstrap 5 has switched to vanilla JavaScript instead of jQuery.

## Why Use Bootstrap?

Advantages of Bootstrap:

- **Easy to use:** Anybody with just basic knowledge of HTML and CSS can start using Bootstrap
- **Responsive features:** Bootstrap's responsive CSS adjusts to phones, tablets, and desktops
- **Mobile-first approach:** In Bootstrap, mobile-first styles are part of the core framework
- **Browser compatibility:** Bootstrap 5 is compatible with all modern browsers (Chrome, Firefox, Edge, Safari, and Opera). 
**Note** that if you need support for IE11 and down, you must use either BS4 or BS3.

## Where to Get Bootstrap 5?
There are two ways to start using Bootstrap 5 on your own web site.

You can:

- Include Bootstrap 5 from a CDN
- Download Bootstrap 5 from getbootstrap.com

### Bootstrap 5 CDN
If you don't want to download and host Bootstrap 5 yourself, you can include it from a CDN (Content Delivery Network).

jsDelivr provides CDN support for Bootstrap's CSS and JavaScript:
```html
<!-- Latest compiled and minified CSS -->  
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">  
  
<!-- Latest compiled JavaScript -->  
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

الأفضل انك تنزله ومتستخدمش الحوار دا غير مثلًا وانت بتتعلم أو كدا 

### Downloading Bootstrap 5

If you want to download and host Bootstrap 5 yourself, go to [https://getbootstrap.com/](https://getbootstrap.com/), and follow the instructions there.

## Create Your First Web Page With Bootstrap 5
**1. Add the HTML5 doctype**
```html
<!DOCTYPE html>  
<html lang="en">  
  <head>  
    <title>Bootstrap 5 Example</title>  
    <meta charset="utf-8">  
  </head>  
</html>
```

**2. Bootstrap 5 is mobile-first**
Bootstrap 5 is designed to be responsive to mobile devices. Mobile-first styles are part of the core framework.

The `width=device-width` part sets the width of the page to follow the screen-width of the device (which will vary depending on the device).

The `initial-scale=1` part sets the initial zoom level when the page is first loaded by the browser.
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

**3. Containers**
Bootstrap 5 also requires a containing element to wrap site contents.

There are two container classes to choose from:

1. The `.container` class provides a responsive **fixed width container**
2. The `.container-fluid` class provides a **full width container**, spanning the entire width of the viewport