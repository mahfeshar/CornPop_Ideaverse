---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-07-23
---

JavaScript APIs are Application Programming Interfaces that use JavaScript scripting to dynamically access and modify content. 
[[API]]
## DOM API
![[Pasted image 20240709120352.png]]

---
![[Pasted image 20240709120433.png]]

---
![[Pasted image 20240709120524.png]]
![[Pasted image 20240709120540.png]]

---
![[Pasted image 20240709120639.png]]

![[Pasted image 20240709120726.png]]

---
![[Pasted image 20240709120836.png]]

---
![[Pasted image 20240709121006.png]]
![[Pasted image 20240709121108.png]]

---
![[Pasted image 20240709121207.png]]

---
![[Pasted image 20240709121347.png]]

---
![[Pasted image 20240709121516.png]]

![[Pasted image 20240709121555.png]]

## REST Architecture
Most JavaScript APIs follow the Representational State Transfer ([[REST API]]) architectural style. 
These are referred to as RESTful APIs, and follow the CRUD paradigm. 
CRUD stands for Create, Read, Update, and Delete, and model the four basic functionalities needed when communicating between services and with a database. 
In a REST environment, these CRUD operations are often aliased as follows:

- Create → POST
- Read → GET
- Update → PUT
- Delete → DELETE

As an example, imagine an API which communicates with a banking service to process online payments. It is possible to use all four CRUD operations for this API. An example of each is provided below.

|Method|URL|Description|
|---|---|---|
|POST|api/customer|Create a new banking customer|
|GET|api/customers/{id}|Retrieve the information of a customer|
|PUT|api/customers/{id}|Update information for a specific customer|
|DELETE|api/customers/{id}|Delete a banking customer|
The URLs in each example are important, as they determine the specific item/customer that is being accessed.

In the POST request, you can see that a new customer is created with the API. 
Depending on the specifications of the API, this may include options to provide data for this customer, such as a name or credit card details. 
It may also automatically generate new information upon creation, such as an id.

The GET request allows you to retrieve all the information associated with a customer. 
The API assumes a unique id for each customer, that is used in the URL to specify which customer’s information you are searching. 
A response for this request can come in many different formats, such as JSON or XML, depending on the API.

In the PUT request, you are able to update the information for a specific customer. This will overwrite the current data with new data. Similar to the GET request, you can specify a specific customer using the id. You can provide new data to be updated in different ways that are specific to the API. Some APIs allow you to include a “body” in which you can specify a load of data to be sent with the request. For example, you can attach the following body to the PUT request in order to update a customer’s first and last name:

```js
{
    "first_name": "Thomas",
    "last_name": "Watson"
}
```
In the DELETE request given in the example, you can remove a customer entirely by once again providing the id.

## XMLHttpRequest
A popular JavaScript API is XMLHttpRequest (XHR), which allows you to retrieve data without refreshing the entire page. This is important when you to want to update only a part of a page without disrupting what a user is currently doing on the page.

XMLHttpRequest is used heavily in Asynchronous JavaScript And XML (AJAX) programming. Full documentation on its usage can be found on (this page)  
[https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)

## Advanced APIs
There are more advanced JavaScript APIs available, each with a different use and specification. Many of these APIs can be found on the [official Mozilla Developer website](https://developer.mozilla.org/en-US/docs/Web/API) or you can search the internet for the required API.