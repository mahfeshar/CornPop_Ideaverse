---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-08-02
---

### تعريف REST API
الـ **REST API** هي طريقة للتواصل بين الأنظمة باستخدام **HTTP**، وده بيخلينا نطلب بيانات، نعدل عليها، أو نحذفها. 
الهدف منها إنها تخلي التواصل بسيط وسريع، وتركز على الموارد (Resources) زي الكائنات والبيانات اللي بنتعامل معاها.

لكي نتواصل مع طرف آخر، يجب أن نحدد ما نريده من الطرف الآخر.هل نريد بيانات معينة؟ هل نمتلك بيانات في الطرف الآخر ونريد تحديثها أو حتى حذفها؟
### الفرق بين REST API والـ API العادي
- الـ **[[API]]** بشكل عام هو أي طريقة تقدر بيها تخلي برنامج يتواصل مع برنامج تاني.
- الـ**REST API** بقى بتمشي على قواعد معينة باستخدام طرق الـ **HTTP** زي:
  - الـ**GET**: لو عايز تجيب بيانات.
  - الـ**POST**: لو عايز تضيف بيانات جديدة.
  - الـ**PUT**: لو عايز تعدل بيانات موجودة بالكامل.
  - الـ**PATCH**: لو عايز تعدل جزء صغير من البيانات.
  - الـ**DELETE**: لو عايز تحذف بيانات.

---

### أهم مكونات REST API
1. الـ**Request (الطلب)**: العميل (Client) بيبعت طلب للسيرفر (Server) زي إنه يجيب بيانات.
2. الـ**Response (الرد)**: السيرفر بيرد على العميل بالبيانات أو الحالة المطلوبة.

---

### مثال عملي
تخيل عندك تطبيق بيع آيس كريم وعايز تعرف النكهات المتاحة وتدي الموظفين صلاحية يضيفوا أو يحذفوا نكهات. 

- لما العميل يطلب النكهات:  
  - الـ**Request**: هو GET على "`/api/flavors`".
  - الـ**Response**: السيرفر يرد بـ **JSON** يحتوي النكهات المتاحة.

- لما الموظف يضيف نكهة جديدة:  
  - الـ**Request**: POST على "`/api/flavors`" مع بيانات النكهة الجديدة.
  - الـ**Response**: السيرفر يرد بتأكيد إضافة النكهة.

---

### هيكل الطلب (Request Structure)
1. الـ**Operation**: زي `GET`, `POST`, `PUT`.
2. الـ**Endpoint**: المكان اللي بتطلب منه الخدمة، زي "`/api/flavors`".
3. الـ**Parameters or Body**: البيانات اللي بتبعتها (لو فيه).
4. الـ**Headers**: زي **API key** أو بيانات التوثيق.

---

### هيكل الرد (Response Structure)
- الرد بيجي غالبًا في صورة **JSON**.
- بيكون فيه كود حالة (Status Code) زي:
  - الـ`200 OK`: الطلب نجح.
  - الـ`201 Created`: تم إنشاء مورد جديد.
  - الـ`404 Not Found`: المورد مش موجود.
  - الـ`500 Internal Server Error`: فيه مشكلة في السيرفر.

---

### القيود الأساسية في REST API
#### 1. Uniform Interface

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

#### 2. Stateless

The server is independent of the client. The server doesn’t store user client information/state. Each request contains enough context to process it (HTTP Headers, etc.)

Some authentication systems like OAuth have to store information on the server side but they do it with REST API design.

#### 3. Cacheable

All server responses (resource representation) are cacheable:

- Explicit
- Implicit
- Negotiated

Caches are here to improve performances. In a REST API, clients don’t care about the caching strategy, if the resource representation comes from a cache or from a database…

#### 4. Client-Server

REST API is designed to separate Client from the Server. The server doesn’t know who is talking to it. Clients are not concerned with data storage => the portability of client code is improved. Servers are not concerned with the user interface or user state so that servers can be simpler and more scalable

#### 5. Layered System

Client can’t assume direct connection to server. Intermediary servers may improve system scalability by enabling load-balancing and by providing shared caches. Layers may also enforce security policies.

#### 6. Code on Demand (optional)

Server can temporarily:

- Transfer logic to client
- Allow client to execute logic
- Example: JavaScript
#### ملخص
1. **Uniform Interface (واجهة موحدة)**  
   - كل الطلبات لها نفس الشكل والقواعد، مما يسهل التعامل معاها.

2. **Stateless (بدون حالة)**  
   - كل طلب مستقل، والسيرفر مش بيحتفظ بمعلومات عن العميل.

3. **Cacheable (يدعم التخزين المؤقت)**  
   - الردود ممكن تتخزن في الكاش لتحسين الأداء.

4. **Client-Server (فصل العميل عن السيرفر)**  
   - العميل ما يعرفش التفاصيل عن السيرفر، والعكس صحيح.

5. **Layered System (نظام متعدد الطبقات)**  
   - الطلبات ممكن تعدي على خوادم وسيطة لتحسين الأداء والأمان.

6. **Code on Demand (اختياري)**  
   - السيرفر ممكن يبعت كود (زي JavaScript) للعميل ينفذه عنده.

---

### الخلاصة
الـ **REST API** بتسهل التواصل بين الأنظمة باستخدام HTTP، وبتمشي على قواعد زي إنها لازم تكون **stateless** وقابلة للتخزين المؤقت. الفكرة إنها تخلي العميل يقدر يتواصل مع السيرفر بسهولة، سواء كان بيجيب بيانات، يضيفها، يعدلها، أو يحذفها.

---

### ملاحظات وتصحيح
- الكلام اللي مكتوب فوق صحيح، لكن مهم تعرف إن الفرق بين **PUT** و **PATCH** إن:
  - **PUT** بيعدل كل البيانات.
  - **PATCH** بيعدل جزء صغير منها.

- الـ**Code on Demand** مش دايمًا بيتم استخدامه في كل الـ REST APIs، فده بيعتبر حاجة **اختيارية** مش إلزامية.

---
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

