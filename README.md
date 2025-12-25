# 📦 Storage System

**Language / 言語**

- 🇬🇧 English
- 🇯🇵 [日本語](./README.ja.md)

---

## 1. What Is This Project?

**Storage System** is an event-driven document storage platform designed to solve a common business problem:

> _“Uploaded files exist, but their content is not effectively usable.”_

The system enables:

- Fast file uploads
- Asynchronous OCR processing
- Search by **file name + file content**
- Scalable architecture without blocking user operations

This repository acts as the **root documentation** and architectural overview of the entire system.

---

## 2. Business Background (Why This Exists)

Many companies store large volumes of documents such as:

- Contracts
- Invoices
- Scanned PDFs
- Internal reports
- User-submitted documents

### Common Business Problems

| Problem                         | Business Impact                |
| ------------------------------- | ------------------------------ |
| Files are stored only as binary | Content is not searchable      |
| OCR is done synchronously       | Upload becomes slow & unstable |
| Processing logic mixed with API | Hard to maintain & scale       |
| Manual document checking        | High operational cost          |

As data grows, these issues lead to:

- Lower employee productivity
- Increased support & operation costs
- Difficulty adding new features (e.g. AI, analytics)

---

## 3. Design Goal

The system was designed with **business scalability** as the primary goal.

### Key Objectives

- Upload must be **fast and reliable**
- Heavy processing must **not block users**
- Extracted content must be **reusable**
- Architecture must support **future expansion**

This is why the system adopts:

- Event-driven architecture
- Clear separation of responsibilities
- Independent scaling of components

---

## 4. High-Level Architecture

```
[ Frontend ]
     |
     v
[ Backend API ]
     |
     |---> Object Storage (File Upload)
     |
     |---> Message Broker (Event)
                |
                v
      [ Content Processor (OCR Worker) ]
```

### Why This Architecture?

- **User experience first**
  Upload finishes immediately, no waiting for OCR

- **Operational safety**
  OCR failures do not affect upload or API availability

- **Scalability**
  Workers can scale independently based on load

---

## 5. Core Flow (End-to-End)

1. User uploads a file via frontend
2. Backend generates a pre-signed upload URL
3. File is uploaded directly to object storage
4. Backend publishes `FileUploaded` event
5. OCR worker extracts text asynchronously
6. `TextExtracted` event is published
7. Extracted content is saved and indexed
8. User can search by file name or content

This design ensures **eventual consistency**, which is acceptable and intentional for document systems.

---

## 6. Repository Structure & Responsibility

This project is split into multiple repositories to reflect real-world team structures.

| Repository                    | Purpose                             |
| ----------------------------- | ----------------------------------- |
| **storage-domain**            | Business rules, entities, use cases |
| **storage-be**                | API, authentication, orchestration  |
| **storage-content-processor** | OCR worker & async processing       |
| **storage-fe**                | User interface & UX                 |

### Why Separate Repositories?

- Clear ownership
- Independent deployment
- Easier testing & refactoring
- Reflects real production environments

---

## 7. Key Design Decisions & Trade-offs

### Event-Driven vs Synchronous OCR

**Chosen:** Event-driven
**Reason:** Improves UX and system stability
**Trade-off:** Eventual consistency instead of immediate results

---

### Domain-Centric Design

**Chosen:** Domain logic isolated from infrastructure
**Reason:** Business rules remain stable even if tech stack changes
**Trade-off:** Slightly more initial design effort

---

### Simple Search (DB-based)

**Chosen:** Database-based search instead of Elasticsearch
**Reason:** Lower operational cost, simpler setup
**Trade-off:** Limited advanced search features (acceptable for current scale)

---

## 8. What This Project Demonstrates

This project is intended to demonstrate:

- Ability to translate business problems into system design
- Understanding of scalable backend architecture
- Event-driven thinking
- Clean separation between business logic and infrastructure
- Practical trade-off decision making

Rather than showcasing a specific framework, the focus is on **design reasoning**.

---

## 9. Who This System Is For (Example Use Cases)

- HR systems handling resumes
- Accounting systems storing invoices
- Internal knowledge bases
- Document-heavy B2B SaaS platforms

---

## 🔗 Related Repositories

- storage-domain
- storage-be
- storage-content-processor
- storage-fe
