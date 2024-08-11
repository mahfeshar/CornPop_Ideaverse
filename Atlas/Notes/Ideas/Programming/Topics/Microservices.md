---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-07-29
---

الـ **Microservices** هي طريقة جديدة لبناء الأنظمة البرمجية بتركز على تقسيم البرامج لوحدات صغيرة كل واحدة لها وظيفة محددة وباستخدام [[API|APIs]] للتواصل بينهم. دي بتساعد الشركات تبقى أكتر مرونة وتشتغل بأسلوب Agile و DevOps.

**أمثلة على الشركات اللي بتستخدم Microservices:**
- Netflix
- Amazon
- Twitter

**الفرق بين Microservices و Monolithic:**
- Monolithic: برنامج واحد كبير، أي تعديل يؤثر على النظام كله.
- Microservices: برامج صغيرة مستقلة، كل واحدة تقدر تتحدث لوحدها.

**مزايا Microservices:**
1. سهولة النشر.
2. سهولة الفهم.
3. قابلية إعادة الاستخدام في الأعمال.
4. سرعة عزل الأعطال.
5. تقليل المخاطر.

**خصائص Microservices:**
1. **Multiple Components:** تقسيم النظام لوحدات صغيرة.
2. **Built For Business:** مصممة حسب احتياجات العمل.
3. **Simple Routing:** استخدام طرق بسيطة للتواصل.
4. **Decentralized:** كل وحدة تدير بياناتها.
5. **Failure Resistant:** تصميم مقاوم للأعطال.
6. **Evolutionary:** تصميم يتطور مع الزمن.

**مزايا وعيوب Microservices:**
- المزايا: سهولة النشر، الاستقلالية، استخدام تقنيات حديثة، سهولة الصيانة.
- العيوب: تعقيد الاختبارات، مشاكل التواصل بين الوحدات، ازدواجية الجهود.

**مستقبل Microservices:**
- لها مستقبل مشرق بسبب المرونة والقدرة على التعامل مع التطبيقات السحابية والأجهزة الحديثة.

## How Microservice Architecture Works

### 1) Monoliths and Conway’s Law

قانون Conway بيقول: “_Organizations which design systems…are constrained to produce designs which are copies of the communication structures of these organizations._” 

تخيل عندك شركة X فيها فريقين: Support و Accounting. 
كل فريق عنده مسؤوليات محددة زي التعامل مع المبالغ المستردة. 
لو اتخذنا القرار إن الـ Support يتعامل مع الخصومات و Accounting يتعامل مع الاستردادات، بنكون حلينا المشكلة بشكل مناسب. 
ولكن لما بتكبر الفرق وتبقى المشاريع كثيرة على نفس الكود، هيبقى صعب على الكل يشتغل في نفس المكان من الكود بدون تعارضات. وفي النهاية ده بيخلي الموضوع زحمة وكأنك عندك مونوليث كبير.

### 2) Microservices: Avoiding the Monoliths

لو عندك تطبيق كبير وعايز تقسيمه لفرق وكود صغير، ممكن تبدأ بتقسيم الحاجات اللي على أطراف التطبيق، اللي مفيش اعتماد عليها. 
في مثالنا، ممكن نفصل الـ Printer و الـ Storage كخدمات خارجية. 
بدل ما الكود الكبير يتقسم بشكل عشوائي، بيبقى أفضل لو تفصل الأجزاء اللي معتمدة عليها أقل.

### 3) Service Objects and Identifying Data

للانتقال من المونوليثات للخدمات، ممكن نستخدم كائنات الخدمة. يعني نبدأ بتنظيم الكود وكأنه جزء من خدمة خارجية. مثلا، عندنا كلاس للـ Job و Service للـ Job، بحيث يكون كل واحد منهم معاه وظيفته المخصصة وبياناته. الكود ده هيبقى جاهز لتحويله لخدمة خارجية، زي ما في Hexagonal Architecture، مركز التطبيق هو الأساس وكل حاجة تانية حوليه.

**كود نموذج للـ Job:**

```ruby
# A class to model a core transaction and execute it

class Job
  def initialize
    @status = 'Queued'
  end

  def do_useful_work
    ...
    @status = 'Finished'
  end

  def finished?
    return @status == 'Finished'
  end

  def ready?
    return @status == 'Queued'
  end
end
```

**كود نموذج للـ JobService والـ JobStatus:**

```ruby
# Service to do useful work and modify a status

class JobService
  def do_useful_work(job_status)
    # تنفيذ العمل المفيد وتغيير الحالة
    job_status.finish!
    return job_status
  end
end

# A model of our Job's status

class JobStatus
  def initialize
    @status = 'Queued'
  end

  def finished?
    return @status == 'Finished'
  end

  def ready?
    return @status == 'Queued'
  end

  def finish!
    @status = 'Finished'
  end
end
```

### 4) Coordination and "Dumb" Pipes

الميكروسيرفيسز تفرق عن SOA التقليدية في إنها تتجنب الآثار الجانبية. 
في Unix، الأنابيب بتستخدم لربط برامج بسيطة ببعض. 
لما تعمل حاجة تشابه الأنابيب دي في الميكروسيرفيسز، لازم كل خدمة تكون بسيطة ومحددة، بدون قواعد معقدة، بحيث تقدر تربطها مع خدمات تانية بسهولة.

```sh
ls | wc -l
```

## SOA vs. Microservices

الـ SOA (Service-Oriented Architecture) كانت في البداية أوسع من الميكروسيرفيسز. 
الميكروسيرفيسز بتستخدم طرق أسرع للتواصل وتجنب التعقيدات اللي في SOA، وبتستخدم قواعد بيانات NoSQL أكتر. 
الميكروسيرفيسز بتحاول تكون مرنة وسريعة لتلبية احتياجات التطبيقات الحديثة.

## The Future of Microservice Architecture

الاستراتيجية دي بتدي فوائد واضحة في تصميم وتنفيذ التطبيقات. 
تكنولوجيا زي REST وSOAP ممكن تحل بعض المشاكل، لكن الميكروسيرفيسز بتحل مشاكل التواصل والتجزئة بشكل أفضل. 
مع زيادة تعقيد التطبيقات، الميكروسيرفيسز هتكون مستقبل قوي بسبب قدرتها على التوسع والتكيف.