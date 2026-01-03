---
title: "Cache invalidation"
date: 2026-01-03
draft: false
---


# 🧹 Cache Invalidation — Study Notes

## 📌 What is Cache Invalidation?

Cache invalidation is the process of removing or updating cached data before it naturally expires, when the original data changes — so users don’t see outdated (“stale”) information.

🎯 **Goal:** Always serve fresh and correct data, not stale cached copies.

---

## 🤯 Why Is It Hard?

- In distributed systems, the same data can be cached in many places (servers, CDNs, browsers).
- Making sure every copy is updated at the right time is complex.

> “There are only two hard things in Computer Science: cache invalidation and naming things.”

---

## 🔁 Common Cache Invalidation Strategies

| Strategy | How It Works | Example Use Case |
|----------|-------------|------------------|
| TTL ⏱️ | Cache expires after a fixed time | Weather updates |
| Write-Through ✍️ | Update cache + DB together | Banking balances |
| Write-Around 🚫 | Write only to DB | Logging systems |
| Pub/Sub 📡 | Events notify caches | Microservices, CDNs |

---

## 🔹 1. Time-To-Live (TTL)

Cache auto-expires after a set time.

**Example:**  
Product price cached for 5 minutes → after expiry, fetch fresh price.

✔ Simple  
❌ May be briefly stale

---

## 🔹 2. Write-Through

Update cache and database together.

✔ Always fresh  
❌ Slower writes

---

## 🔹 3. Write-Around

Write to DB only, cache updated later on read.

✔ Efficient for heavy writes  
❌ First read is slow

---

## 🔹 4. Publish / Subscribe

Services notify others when data changes.

✔ Best for distributed systems  
❌ More complex

---

## ⚠️ Challenges

| Problem | Explanation |
|--------|-------------|
| Multiple caches | Same data everywhere |
| Network delays | Invalidation lag |
| Partial failures | Missed updates |
| CDN complexity | Hard to sync globally |

---

## 🧠 Use Cases

| System | Strategy |
|--------|----------|
| News sites | TTL |
| Banking | Write-Through |
| Logging | Write-Around |
| Microservices | Pub/Sub |
| CDNs | TTL + API |

---

## 📝 One-Line Summary

Cache invalidation keeps cached data fresh by refreshing or removing stale entries using strategies like TTL, write-through, and event-based updates.

---

## 💡 Memory Tips

- TTL = Time-based
- Write-Through = Always fresh
- Write-Around = Fast writes
- Pub/Sub = Distributed sync
