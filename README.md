# Document Me

**Document Me** is a real-time collaborative document editor inspired by **Google Docs**, built to explore modern collaboration technologies like **CRDTs**, **WebSockets**, and scalable backend design.

This project focuses on **system design, realtime collaboration, and clean architecture**, rather than flashy UI or production deployment.

---

## 📌 Overview

Document Me allows multiple users to edit the same document simultaneously with near real-time synchronization.

This repository is the **parent (meta) repository** that provides:
- System overview and architecture
- Technology stack explanation
- Database design and data flow
- Links to all related repositories

Each major component of the system lives in its **own repository** to maintain clear separation of concerns.

---

## 🏗️ System Architecture

The system is composed of four main layers:

- **Angular** frontend for user interaction and editor UI
- **ASP.NET Core (.NET 8)** backend for authentication, APIs, and persistence
- **Hocuspocus (Yjs)** server for realtime collaboration
- **PostgreSQL** for persistent storage

```text
Angular Frontend
      |
      | REST APIs + JWT / Secure Cookies
      v
.NET Backend API
      |
      | WebSocket (Yjs / CRDT updates)
      v
Hocuspocus Realtime Server
      |
      v
PostgreSQL Database
