---
up:
  - "[[SOLID Principles]]"
related: 
created: 2024-07-11
---
### Single Responsibility Principle

ال **Single Responsibility Principle** بيقول إن الكلاس لازم يكون ليها سبب واحد إنها تتغير. بمعنى:

- ماينفعش يكون عندي كلاس بتعمل أكتر من حاجة في نفس الوقت.
- مش محتاجين **Multitasking** في الكلاسات.

ليه ماينفعش؟ لأن ده مع الوقت هيعقد الأبليكيشن، ولو حصل تغيير في حاجة واحدة في الكلاس دي، ممكن يأثر على حاجات تانية فيها.

#### مثال بسيط

تعالوا نشوف مثال بسيط يوضح الفكرة. عندنا كود ما بيدعمش **Single Responsibility Principle**:
```java
public class EmailService {
    public void sendEmail(String recipient, String message) {
        // SMTP server logic to send email
    }

    public String loadTemplate(String templateName) {
        // Load email template logic
    }

    public void updateTemplate(String templateName, String newContent) {
        // Update email template logic
    }
}
```

الكلاس دي بتعمل 3 حاجات:

1. تبعت إيميلات.
2. تلود الإيميل تمبلت.
3. تأبديت الإيميل تمبلت.

المفروض نفصل كل حاجة من دول في كلاس لوحدها.

#### الحل: تحقيق Single Responsibility Principle

هنفصل الكلاس دي لعدة كلاسات، كل كلاس بتقوم بوظيفة واحدة:

1. **EmailSender**:

```java
public class EmailSender {
    public void sendEmail(String recipient, String message) {
        // SMTP server logic to send email
    }
}
```

2. **TemplateLoader**:
```java
public class TemplateLoader {
    public String loadTemplate(String templateName) {
        // Load email template logic
    }
}

```

3. **TemplateUpdater**:
```java
public class TemplateLoader {
    public String loadTemplate(String templateName) {
        // Load email template logic
    }
}
```

بكده لو عايز أغير أي حاجة في إرسال الإيميلات هروح لكلاس **EmailSender** بس، ولو عايز أغير في تحميل التمبلت هروح لكلاس **TemplateLoader**، وهكذا.

#### مثال عملي

خلينا نشوف مثال عملي تاني. عندنا كلاس **OrderManager** بيقوم بعدة وظائف:

```java
public class OrderManager {
    public void processOrder(Order order) {
        // Process the order
    }

    public void processPayment(Payment payment) {
        // Process the payment
    }

    public void sendOrderNotification(String recipient) {
        // Send order notification
    }
}
```

هنفصل الكلاس دي لعدة كلاسات، كل كلاس تقوم بوظيفة واحدة:

1. **OrderProcessor**:

```java
public class OrderProcessor {
    public void processOrder(Order order) {
        // Process the order
    }
}
```

2. **PaymentProcessor**:
```java
public class PaymentProcessor {
    public void processPayment(Payment payment) {
        // Process the payment
    }
}
```

3. **NotificationService**:

```java
public class NotificationService {
    public void sendOrderNotification(String recipient) {
        // Send order notification
    }
}
```

بكده لو عايز أغير أي حاجة في معالجة الطلبات هروح لكلاس **OrderProcessor**، ولو عايز أغير في معالجة الدفع هروح لكلاس **PaymentProcessor**، ولو عايز أغير في إرسال الإشعارات هروح لكلاس **NotificationService**.

### الخلاصة

ال **Single Responsibility Principle** بيقول إن كل كلاس لازم يكون ليها سبب واحد للتغيير. ده بيخلي الكود أبسط وأسهل في الصيانة والتطوير، وبيقلل من المشاكل اللي ممكن تحصل بسبب التعقيدات.