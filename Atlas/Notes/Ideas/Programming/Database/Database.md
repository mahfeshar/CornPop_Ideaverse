---
up:
  - "[[Database MOC]]"
related:
  - "[[Database Management System (DBMS)]]"
created: 2024-05-21
---
## What are databases for?
البرنامج بتاعنا بياخد Input وبيعمل Process ليها وبيطلع Output بس كل دا بيحصل في الميموري وبمجرد ما البرنامج يقفل الداتا دي بتطير
فيه برامج مش بيفرق معانا اننا نخزن الداتا دي عادي (الآلة حاسبة) 
وفيه برامج لا محتاج أخزن الداتا دي (تسجيل كورسات)

![[Pasted image 20241105120657.png]]
- Storing data in your application (in memory) has the obvious shortcoming that, whatever the technology you’re using, **your data dies when your server stops**. 
- Some programming languages and/or frameworks take it even further by being **stateless**, which, in the case of an HTTP server, means your data dies at the end of an HTTP request. 
- Whether the technology you’re using is stateless or stateful, you will need to persist your data somewhere. That’s what databases are for.

## Data vs Information
Data: شوية البيانات اللي انا **بجمعها**
Information: لما بعمل على الداتا بروسيسينج بتتحول لمعلومة

مثال: تاريخ الميلاد يعتبر **Data** هعمل عليه Process فهيتحول لعمر فدي **Information**
## Database
- It's for everyone (Backend Developer, Mobile Application Developer, Data Scientist).
- A __database__ is a collection of data, typically describing the activities of one or more related organizations.
- A __database__ _models_ some aspect of the real world (student, course)
- A database can be of __any size__ or __complexity__

## Database is __acid__
- **A**tomicity: transactions are atomic, which means if a transaction fails, the result will be like it never happened.
- **C**onsistency: you can define rules for your data, and expect that the data abides by the rules, or else the transaction fails.
- **I**solation: run two operations at the same time, and you can expect that the result is as though they were ran one after the other. 
  That’s not the case with the JSON file storage you built: if 2 insert operations are done at the same time, the later one will fetch an outdated collection of users because the earlier one is not finished yet, and therefore overwrite the file without the change that the earlier operation made, totally ignoring that it ever happened.
- **D**urability: unplug your server at any time, boot it back up, and it didn’t lose any data.

## __ACID__ is a cool acronym! [[CRUD]] is another cool one
## [[Database Management System (DBMS)]]
