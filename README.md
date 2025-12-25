## 📦 Storage System

[English](./README.md) | [日本語](./README.ja.md)

---

### 🔍 Overview

**Storage System** is a document storage platform that allows users to **search files not only by file name, but also by file content** using **OCR (Optical Character Recognition)**.

This system is designed to solve a common problem in document management:

> _Files are stored digitally, but their contents are effectively invisible._

---

### ❗ Problem Statement

In many organizations:

- 📁 Files are stored as **PDFs, images, or scanned documents**
- 🔎 Search is limited to **file names or metadata**
- 🧾 Important information inside documents **cannot be searched**
- ⏱️ Finding the right document becomes **slow and inefficient**

---

### 💡 Solution

Storage System extracts and indexes **text inside files** using OCR, enabling:

- 🔎 Search by **file name**
- 📄 Search by **file content**
- ⚡ Faster document discovery
- 🧠 Better use of stored data

---

### 🧱 System Architecture

The system is split into multiple repositories to keep responsibilities clear and maintainable:

| Repository                       | Responsibility                          |
| -------------------------------- | --------------------------------------- |
| 🧩 **storage-system**            | Project overview & system documentation |
| 🧠 **storage-domain**            | Core business rules and domain logic    |
| ⚙️ **storage-be**                | Application layer & APIs                |
| 🛠️ **storage-content-processor** | OCR worker & content extraction         |
| 🎨 **storage-fe**                | User interface                          |

> This separation follows clean architecture principles to keep business logic independent and scalable.

---

### 🔄 High-Level Flow

1. 📤 User uploads a file
2. ⚙️ Backend stores file metadata
3. 🛠️ OCR worker extracts text from file content
4. 🧠 Extracted text is indexed
5. 🔍 User can search by **file name or content**

---

### 🎯 Goals

- Make document content **searchable**
- Separate **business logic**, **application logic**, and **infrastructure**
- Enable future scalability (new processors, search engines, storage backends)

---

### 📚 Related Repositories

- [`storage-domain`](https://github.com/wiwiewei18/storage-domain)
- [`storage-be`](https://github.com/wiwiewei18/storage-be)
- [`storage-content-processor`](https://github.com/wiwiewei18/storage-content-processor)
- [`storage-fe`](https://github.com/wiwiewei18/storage-fe)

---

### 🌍 Language

- 🇬🇧 English (current)
- 🇯🇵 Japanese → [README.ja.md](./README.ja.md)
