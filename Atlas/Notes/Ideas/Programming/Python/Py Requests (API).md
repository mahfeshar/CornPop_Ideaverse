---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-29
---
عشان تتعامل مع API في Python، هتحتاج تستخدم مكتبات مختلفة بناءً على نوع الـ API اللي بتتعامل معاه. أكتر مكتبة مستخدمة للتعامل مع APIs في Python هي `requests`.

### 1. **تثبيت مكتبة `requests`:**

أول حاجة، لازم تثبت مكتبة `requests` لو مش مثبتة عندك. تقدر تثبتها باستخدام `pip`:

```bash
pip install requests
```

### 2. **عمل طلب (Request) إلى API:**

تقدر تستخدم مكتبة `requests` لعمل طلبات HTTP مختلفة زي GET و POST و PUT و DELETE. 
#### **طلب GET:**

ده نوع من الطلبات اللي بنستخدمه عشان نجيب بيانات من الـ API.

```python
import requests

# Address for API
url = 'https://api.example.com/data'

# GET
response = requests.get(url)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

- الـ **`response.json()`**: بتحول الاستجابة إلى JSON عشان تقدر تتعامل معها ككائن Python.

#### **طلب POST:**

ده بنستخدمه عشان نبعت بيانات إلى الـ API.

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data'

# البيانات اللي عايز تبعتها
payload = {
    'key1': 'value1',
    'key2': 'value2'
}

# عمل طلب POST
response = requests.post(url, json=payload)

# التأكد من حالة الاستجابة
if response.status_code == 201:
    # عرض البيانات الجديدة
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

- **`json=payload`**: بتحول البيانات إلى JSON وتبعتها في الجسم (body) للطلب.

#### **طلب PUT:**

ده بنستخدمه لتحديث بيانات موجودة في الـ API.

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data/1'

# البيانات اللي عايز تحدثها
payload = {
    'key1': 'new_value1',
    'key2': 'new_value2'
}

# عمل طلب PUT
response = requests.put(url, json=payload)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات المحدثة
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

#### **طلب DELETE:**

ده بنستخدمه لحذف بيانات موجودة في الـ API.

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data/1'

# عمل طلب DELETE
response = requests.delete(url)

# التأكد من حالة الاستجابة
if response.status_code == 204:
    print("Deleted successfully")
else:
    print(f"Error: {response.status_code}")
```

### 3. **التعامل مع الأخطاء:**

مكتبة `requests` توفر لك وسيلة للتحقق من الأخطاء باستخدام الكودات الخاصة بالاستجابة (status codes). بعض الأكواد الشائعة:

- **200 OK**: الطلب تم بنجاح.
- **201 Created**: البيانات اتخلقت بنجاح.
- **204 No Content**: البيانات اتحذفت بنجاح.
- **400 Bad Request**: الطلب كان فيه مشكلة.
- **401 Unauthorized**: لازم تسجل دخول.
- **404 Not Found**: المورد اللي طلبته غير موجود.
- **500 Internal Server Error**: حصل خطأ في الخادم.

### 4. **إضاف (Headers) و(Parameters):**

#### **إضافة Headers:**

```python
import requests

url = 'https://api.example.com/data'
headers = {
    'Authorization': 'Bearer YOUR_API_TOKEN',
    'Content-Type': 'application/json'
}

response = requests.get(url, headers=headers)
```

**الـ Headers** هي معلومات إضافية تُرسل مع طلبات (requests) واستجابات (responses) HTTP لتوفير معلومات عن الطلب أو الاستجابة. 
الـ Headers بتساعد في التحكم في كيفية معالجة الطلبات والاستجابات، وتوفر معلومات عن نوع البيانات، الترخيص، التشفير، وغيرها.

##### **أنواع الـ Headers**

1. الـ**Content-Type**: يحدد نوع البيانات اللي بتبعتها في الطلب. مثلاً، `application/json` لو كنت بترسل بيانات بصيغة JSON.
   
2. الـ**Authorization**: يُستخدم لتوفير بيانات التوثيق، مثل رموز التوكن (tokens) أو مفاتيح API (API keys) للوصول إلى الموارد المحمية.

3. الـ**Accept**: يحدد نوع البيانات اللي تتوقعها في الاستجابة. مثلاً، `application/json` لطلب استجابة بصيغة JSON.

4. الـ**User-Agent**: يحدد نوع ومتصفح العميل (client) الذي يقوم بإرسال الطلب.

5. الـ**Cache-Control**: يتحكم في كيفية تخزين البيانات في الكاش.

6. الـ**Authorization**: يُستخدم لتوفير بيانات التوثيق، مثل رموز التوكن (tokens) أو مفاتيح API (API keys) للوصول إلى الموارد المحمية.

##### **كيفية استخدام الـ Headers في طلبات HTTP باستخدام مكتبة `requests`**

###### **1. إضافة Headers إلى طلب GET:**

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data'

# إعداد الـ Headers
headers = {
    'Authorization': 'Bearer YOUR_API_TOKEN',
    'Accept': 'application/json'
}

# عمل طلب GET مع الـ Headers
response = requests.get(url, headers=headers)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

###### **2. إضافة Headers إلى طلب POST:**

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data'

# البيانات اللي هتبعتها
payload = {
    'key1': 'value1',
    'key2': 'value2'
}

# إعداد الـ Headers
headers = {
    'Authorization': 'Bearer YOUR_API_TOKEN',
    'Content-Type': 'application/json'
}

# عمل طلب POST مع الـ Headers والبيانات
response = requests.post(url, json=payload, headers=headers)

# التأكد من حالة الاستجابة
if response.status_code == 201:
    # عرض البيانات الجديدة
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

###### **3. إضافة Headers إلى طلب PUT:**

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data/1'

# البيانات اللي هتحدثها
payload = {
    'key1': 'new_value1',
    'key2': 'new_value2'
}

# إعداد الـ Headers
headers = {
    'Authorization': 'Bearer YOUR_API_TOKEN',
    'Content-Type': 'application/json'
}

# عمل طلب PUT مع الـ Headers والبيانات
response = requests.put(url, json=payload, headers=headers)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات المحدثة
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

###### **4. إضافة Headers إلى طلب DELETE:**

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data/1'

# إعداد الـ Headers
headers = {
    'Authorization': 'Bearer YOUR_API_TOKEN'
}

# عمل طلب DELETE مع الـ Headers
response = requests.delete(url, headers=headers)

# التأكد من حالة الاستجابة
if response.status_code == 204:
    print("Deleted successfully")
else:
    print(f"Error: {response.status_code}")
```

##### **خلاصة:**
- **الـ Headers** تُستخدم لتوفير معلومات إضافية عن الطلب أو الاستجابة.
- الـ**Content-Type** و **Authorization** و **Accept** من بين أكثر الـ Headers استخدامًا.
- باستخدام مكتبة `requests` في Python، تقدر تضيف الـ Headers بسهولة باستخدام معلمة `headers` في طلبات GET و POST و PUT و DELETE.
#### **إضافة Parameters:**
أيوة، ممكن تضيف باراميتر للطلب من نوع GET عشان تجيب بيانات بناءً على ID أو أي قيمة أخرى. 
في الـ APIs، الباراميترز غالبًا بتكون جزء من الاستعلام (query parameters) في عنوان URL. 

##### 1. **استخدام باراميترز في طلب GET**

افترض أنك عايز تعمل طلب GET للحصول على بيانات لمورد معين بناءً على ID. 
الباراميتر هيكون في الاستعلام. 
في المثال التالي، هنعمل طلب GET لواجهة برمجة التطبيقات (API) ونعطيها ID للبحث عن المورد.

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data'

# الباراميتر اللي عايز تبعته، مثل ID
params = {
    'id': 12345
}

# عمل طلب GET مع الباراميتر
response = requests.get(url, params=params)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

##### 2. **استخدام الباراميتر في عنوان URL مباشرةً**

بعض الأحيان، ممكن تلاقي أن الباراميتر جزء من عنوان URL نفسه بدل من استخدام الاستعلام. 
في هذه الحالة، تكون كالتالي:

```python
import requests

# عنوان الـ API مع الباراميتر مباشرةً في الـ URL
url = 'https://api.example.com/data/12345'

# عمل طلب GET
response = requests.get(url)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

##### 3. **التعامل مع أكثر من باراميتر**

إذا كنت تحتاج تبعت أكثر من باراميتر، ممكن تضيفهم كقائمة من القيم في قاموس الباراميتر:

```python
import requests

# عنوان الـ API
url = 'https://api.example.com/data'

# أكثر من باراميتر
params = {
    'id': 12345,
    'type': 'user'
}

# عمل طلب GET مع الباراميتر
response = requests.get(url, params=params)

# التأكد من حالة الاستجابة
if response.status_code == 200:
    # عرض البيانات
    data = response.json()  # تحويل الاستجابة إلى JSON
    print(data)
else:
    print(f"Error: {response.status_code}")
```

##### **خلاصة:**

- لتقديم باراميتر في طلب GET، استخدم خاصية `params` في مكتبة `requests`، وضع فيها القيم التي تريد إرسالها.
- الباراميتر ممكن يكون جزء من عنوان URL مباشرةً أو في الاستعلام كقيمة key-value.

باستخدام الطرق دي، تقدر تجيب البيانات بناءً على ID أو أي باراميتر آخر يحتاجه الـ API.
### **خلاصة:**

التعامل مع API في Python سهل باستخدام مكتبة `requests`. 
تقدر تعمل طلبات GET و POST و PUT و DELETE، وتتعامل مع الأخطاء وتضيف رؤوس وباراميترز حسب الحاجة. 
باستخدام المكتبة دي، هتقدر تدمج البيانات من APIs في تطبيقاتك بكل سهولة.