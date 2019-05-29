---
title: git error
date: 2019-05-27 09:05:10
category: development
---

Git push가 안되는 경우 (fatal: refusing to merge unrelated histories)
서로 관련 기록이 없는 두 프로젝트를 병합할 때 허용

```bash
git pull origin master --allow-unrelated-histories
```
