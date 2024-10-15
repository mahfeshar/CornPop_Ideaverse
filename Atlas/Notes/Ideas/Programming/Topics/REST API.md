---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-08-02
---

- الـ REST API هو نفس الـ [[API]] بالضبط، لكن مع بعض الإضافات البسيطة. 
  لكي نتواصل مع طرف آخر، يجب أن نحدد ما نريده من الطرف الآخر.هل نريد بيانات معينة؟ هل نمتلك بيانات في الطرف الآخر ونريد تحديثها أو حتى حذفها؟

بنستخدم طرق الـ HTTP لما باجي أعمل Request
الـ REST API يمكننا من تحديد نوع الطلبية التي نريد إرسالها إلى الطرف الآخر. وهناك خمسة أنواع من الطلبات:
1. **GET**: للحصول على بيانات.
2. **POST**: لإرسال بيانات.
3. **PUT**: لتعديل بيانات.
4. **PATCH**: لتحديث جزء من البيانات.
5. **DELETE**: لحذف بيانات.
- الفرق بينها وبين الـ [[API]] العادي، ان لازم تحدد انت عايز ايه بالظبط من الطرف التاني 
  لو عندي داتا في الطرف التاني، عايز منها ايه بالظبط 
  (أخذ GET - تحديث PUT - حذف DELETE - إضافة POST)
- الإتنين يعتبروا فكرة واحدة

## REST API
REST API is a software architectural style for Backend.

**REST = “REpresentational State Transfer”.** **API = Application Programming Interface**

Its purpose is to induce performance, scalability, simplicity, modifiability, visibility, portability, and reliability.

REST API is **Resource-based**, a resource is an object and can be access by a URI. An object is “displayed”/transferred via a **representation** (typically JSON). HTTP methods will be actions on a resource.

Example:

- Resource: `Person` (John)
- Service: contact information (`GET`)
- Representation:
    - `first_name`, `last_name`, `date_of_birth`
    - JSON format

## عمل REST API
#### ملفات المشروع

لدينا عدة ملفات مهمة في المشروع:

- **Route**: يستقبل الطلبيات ويوصلها.
- **Controller**: ينفذ العمليات على الطلبيات.
- **Model**: يخزن النتيجة النهائية في قاعدة البيانات.

#### مثال عملي

لنفترض أن المستخدم يريد تسجيل الدخول إلى الموقع بإدخال البريد الإلكتروني. سنأخذ البريد الإلكتروني هذا ونرسله إلى قاعدة البيانات عبر عملية **POST**.

1. البريد الإلكتروني يُرسل عبر **POST** إلى قاعدة البيانات.
2. قاعدة البيانات تستقبل البريد الإلكتروني وترسله إلى ملف **Controller**.
3. الـ Controller يعدل على الطلبية، يضيف أو يحذف منها، ثم يرسلها إلى ملف **Model**.
4. الـ Model يخزن البيانات في قاعدة البيانات ويرد باستجابة لتأكيد ما إذا كانت العملية ناجحة أم لا.
## الشرح بمثال
### مثال بسيط:
تخيل إنك شغال في محل آيس كريم وعاوز تعمل تطبيق ويب يعرض نكهات الآيس كريم اللي موجودة وتسمح للموظفين يحدثوا النكهات. 
إزاي تعمل كده؟ باستخدام REST API.

### تعريف REST API:
الـ REST بترمز لـ "Representational State Transfer". هو نوع من الـ API مشهور ومستخدم في الصناعة.

### فوايد REST API:
1. **التواصل السهل:** بيستخدم طريقة موحدة للتواصل بين العميل والسيرفر.
2. **قابلية التوسع والـ stateless:** الخدمة تقدر تكبر وتتعقد بسهولة، ومفيش حاجة تتسجل أو تتبعها بين العميل والسيرفر.
3. **أداء عالي:** بيدعم الـ caching اللي بيحسن الأداء مع تعقد الخدمة.

### مثال عملي:
لو عندنا endpoint زي "`icecream.com/api/flavors`، 
الـ `api` دي بتشير لجزء الـ API، و"flavors" دي اسم الـ resource.

### مكونات الـ REST API:
1. **Request:** الطلب اللي العميل بيبعت للسيرفر.
2. **Response:** الرد اللي السيرفر بيرده للعميل.

### [[CRUD]] Operations:
1. **Create:** باستخدام "POST".
2. **Read:** باستخدام "GET".
3. **Update:** باستخدام "PUT".
4. **Delete:** باستخدام "DELETE".

### هيكل الـ Request:
1. الـ**Operation:** زي POST أو GET.
2. الـ**Endpoint:** زي "`/api/flavors`".
3. الـ**Parameters or Body:** البيانات اللي بتبعتها في الطلب.
4. الـ **Headers:** ممكن يكون فيها API key أو بيانات التوثيق.

### هيكل الـ Response:
بيكون عادة في صورة [[JSON]].

### سيناريوهات:
1. **عرض النكهات المتاحة:**
   - **Request:** GET على "/api/flavors".
   - **Response:** array بالنكهات المتاحة.

2. **تحديث نكهة:**
   - **Request:** PUT على "/api/flavors/1" مع بيانات النكهة الجديدة.
   - **Response:** تأكيد بتحديث النكهة.

3. **إضافة نكهة جديدة:**
   - **Request:** POST على "/api/flavors" مع بيانات النكهة الجديدة.
   - **Response:** تأكيد بإضافة النكهة الجديدة.

## There are 6 constraints:

### 1. Uniform Interface

- Define the interface between client-server
- Simple and can be split in small parts

#### HTTP verbs

- `GET`:
    - Read representation of a resource or a list of resources
- `POST`:
    - Create a new resource
- `PUT`:
    - Update an existing resource
- `DELETE`:
    - Remove an existing resource

#### URIs - resource name

A resource representation is accessible by a URI:

- `GET /users`: path for listing all user resources
- `GET /users/12`: path for the user `id = 12`
- `GET /users/12/addresses`: path for listing all addresses of the user `id = 12`
- `POST /users`: path for creating a user resource
- `PUT /users/12`: path for updating the user `id = 12`
- `DELETE /users/12/addresses/2`: path for deleting the address `id = 2` of the user `id = 12`

#### HTTP Response

In the HTTP Response, the client should verify the information of two things:

- status code: result of the action
- body: JSON or XML representation of resources

Some important status code:

- `200`: OK
- `201`: created => after a `POST` request
- `204`: no content => can be return after a `DELETE` request
- `400`: bad request => the server doesn’t understand the request
- `401`: unauthorized => client user can’t be identified
- `403`: forbidden => client user is identified but not allowed to access a resource
- `404`: not found => resource doesn’t exist
- `500`: internal server error

### 2. Stateless

The server is independent of the client. The server doesn’t store user client information/state. Each request contains enough context to process it (HTTP Headers, etc.)

Some authentication systems like OAuth have to store information on the server side but they do it with REST API design.

### 3. Cacheable

All server responses (resource representation) are cacheable:

- Explicit
- Implicit
- Negotiated

Caches are here to improve performances. In a REST API, clients don’t care about the caching strategy, if the resource representation comes from a cache or from a database…

### 4. Client-Server

REST API is designed to separate Client from the Server. The server doesn’t know who is talking to it. Clients are not concerned with data storage => the portability of client code is improved. Servers are not concerned with the user interface or user state so that servers can be simpler and more scalable

### 5. Layered System

Client can’t assume direct connection to server. Intermediary servers may improve system scalability by enabling load-balancing and by providing shared caches. Layers may also enforce security policies.

### 6. Code on Demand (optional)

Server can temporarily:

- Transfer logic to client
- Allow client to execute logic
- Example: JavaScript