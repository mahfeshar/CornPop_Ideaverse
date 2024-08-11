---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---
Happened because you didn't clone the repo with your token.
Keep it in mind to always clone your repos with your token in case of next time.

```git
git clone https://<token>@github.com/<username>/<repo>.git

git clone https://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@github.com/mahfeshar/alx-system_engineering-devops.git

git clone https://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@github.com/mahfeshar/alx-higher_level_programming.git
```

The solution if you forget:

```git
git remote set-url origin https://<username>:<token>@github.com/<username>/<repo>.git
```

```git
git remote set-url origin https://mahfeshar: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@github.com/mahfeshar/alx-higher_level_programming.git

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
```
