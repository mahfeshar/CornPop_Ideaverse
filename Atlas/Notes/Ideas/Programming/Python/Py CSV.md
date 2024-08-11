---
up:
  - "[[Programming MOC]]"
  - "[[Python MOC]]"
related: 
created: 2024-07-29
Link: https://www.scaler.com/topics/how-to-create-a-csv-file-in-python/
---

### 1. **مقدمة عن CSV:**

- الـ**CSV** هو اختصار لـ **Comma-Separated Values**، وهو نوع من الملفات اللي بتخزن البيانات بشكل جداول، كل قيمة فيها مفصولة عن التانية بفاصلة.
- البيانات بتبقى عبارة عن صفوف وأعمدة، وده بيخليها سهلة للقراءة والتعديل.
- بنتعامل مع [[Py File Handling]]
### 2. **إزاي تستخدم مكتبة `csv` في Python:**

#### **1. قراءة ملف CSV:**
أول حاجة، لو عايز تقرأ بيانات من ملف CSV، ممكن تستخدم الكود التالي:

```python
import csv

with open('data.csv', mode='r') as file:
    csv_reader = csv.reader(file)
    for row in csv_reader:
        print(row)
```

- الـ`import csv`: هنا بتستورد مكتبة `csv`.
- الـ `with open('data.csv', mode='r') as file`: بيفتح الملف `data.csv` في وضع القراءة.
- الـ `csv.reader(file)`: بيستخدم `csv.reader` لقراءة محتويات الملف.
- الـ`for row in csv_reader`: هنا بتستخدم حلقة `for` عشان تمر على كل صف في الملف وتطبعه.

#### **2. كتابة ملف CSV:**
لو عايز تكتب بيانات في ملف CSV، استخدم الكود ده:

```python
import csv

data = [
    ['Name', 'Age', 'City'],
    ['Alice', '30', 'New York'],
    ['Bob', '25', 'Los Angeles']
]

with open('data.csv', mode='w', newline='') as file:
    csv_writer = csv.writer(file)
    csv_writer.writerows(data)
```

- الـ`data = [...]`: هنا بتحدد البيانات اللي عايز تكتبها في الملف. البيانات بتكون عبارة عن [[Py list]] of Lists، وكل list تمثل صف في الجدول.
- الـ`with open('data.csv', mode='w', newline='') as file`: بيفتح الملف `data.csv` في وضع الكتابة.
- الـ`csv.writer(file)`: بيستخدم `csv.writer` لكتابة البيانات في الملف.
- الـ`csv_writer.writerows(data)`: بيدوّن جميع الصفوف من `data` في الملف.

#### **3. التعامل مع الأعمدة:**

ممكن كمان تتعامل مع الأعمدة بشكل منفصل لو عايز، باستخدام `DictReader` و `DictWriter` لو البيانات في شكل قواميس (dictionaries).

- **قراءة بيانات كقاميس:**

```python
import csv

with open('data.csv', mode='r') as file:
    csv_reader = csv.DictReader(file)
    for row in csv_reader:
        print(row)
```

- **كتابة بيانات كقاميس:**

```python
import csv

data = [
    {'Name': 'Alice', 'Age': '30', 'City': 'New York'},
    {'Name': 'Bob', 'Age': '25', 'City': 'Los Angeles'}
]

with open('data.csv', mode='w', newline='') as file:
    fieldnames = ['Name', 'Age', 'City']
    csv_writer = csv.DictWriter(file, fieldnames=fieldnames)
    csv_writer.writeheader()
    csv_writer.writerows(data)
```

- `fieldnames = [...]`: هنا بتحدد أسماء الأعمدة.
- `csv_writer.writeheader()`: بيكتب رؤوس الأعمدة في بداية الملف.

### 3. **نصائح وأفضل الممارسات:**

- **استخدم `newline=''` عند فتح الملفات للكتابة** عشان تتجنب مشاكل مع الفواصل.
- **حافظ على تنسيق البيانات**، لو البيانات فيها فواصل، لازم تتأكد إنها محاطة بعلامات اقتباس.