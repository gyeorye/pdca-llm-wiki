<%*
const today = tp.date.now("YYYY-MM-DD");
const title = await tp.system.prompt("책 제목");
const author = await tp.system.prompt("저자");
-%>
---
tags: [reading, book-raw]
domain: meta
type: book-raw
title: <% title %>
author: <% author %>
started: <% today %>
finished: 
status: reading
confidence: medium
created: <% today %>
updated: <% today %>
---

# <% title %> — Raw Note

> 이 파일은 **raw 원본** (`10-raw/`). LLM이 수정하지 않는다.  
> 완독 후 "이 책 ingest해줘" 요청 → `20-wiki/meta/concepts/`에 개념 노트 생성됨.

## 📖 서지
- **저자**: <% author %>
- **원제**: 
- **역자**: 
- **출판사**: 
- **쪽수**: 
- **난이도**: ⭐ / ⭐⭐ / ⭐⭐⭐ / ⭐⭐⭐⭐ / ⭐⭐⭐⭐⭐

---

## 🎯 왜 읽는가 (시작 전 작성)

> 이 책에서 답을 찾고 싶은 질문 2-3개.

- 
- 
- 

---

## 📝 인용과 메모 (읽으며 자유롭게)

### Chapter 1. 
> 인용

메모: 

### Chapter 2. 
> 인용

메모: 

<!-- 읽으며 계속 추가 -->

---

## 💡 One Big Takeaway (완독 후 1줄)
> 

---

## ❓ 새로 생긴 질문
- 

## 🔗 연결 감지 (다른 책·경험·개념)
- 

## ✅ 행동 (이 책 때문에 할 것)
<!-- `- [ ] You:`로 시작하는 항목은 ingest 시 daily note에 자동 등록 가능 -->
- [ ] 
- [ ] 

---

## 📌 Ingest 요청 문구 (완독 후)

```
{이 파일 경로} 읽고 ingest해줘.
```
