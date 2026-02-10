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

```

## 🧰 Tech Stack

| Layer | Technology |
|------|------------|
| Frontend | Angular 21 |
| Backend | ASP.NET Core (.NET 8) |
| Realtime Engine | Hocuspocus |
| CRDT | Yjs |
| Editor | Tiptap |
| Database | PostgreSQL |
| ORM | Entity Framework Core |
| Authentication | JWT + HttpOnly Secure Cookies |


## 📂 Repositories

This project is organized as multiple repositories to ensure clear separation of concerns.

| Component | Description | Repository |
|----------|------------|------------|
| Backend API | Authentication, REST APIs, persistence logic | 🔗 [Backend Repository](https://github.com/Balasubramanya777/document-me-.net) |
| Frontend | Angular application with collaborative editor | 🔗 [Frontend Repository](https://github.com/Balasubramanya777/document-me-angular) |
| Realtime Server | Realtime collaboration using Yjs & Hocuspocus | 🔗 [Realtime Server Repository](https://github.com/Balasubramanya777/document-me-hocuspocus) |


## 🔄 Data Flow

1. User edits content in the Angular frontend using the Tiptap editor
2. Changes are represented as CRDT updates using Yjs
3. Updates are transmitted to the Hocuspocus server via WebSocket
4. Hocuspocus synchronizes document state across connected clients
5. Backend periodically persists updates and snapshots to PostgreSQL
6. On reload, document state is reconstructed from snapshots and updates


## 🔐 Security Considerations

- Authentication handled using JWT
- Tokens stored using HttpOnly secure cookies
- REST APIs protected via authentication middleware
- WebSocket connections validated at the server level
- Permanent deletes executed within database transactions
- No secrets or credentials committed to repositories


## 🚀 Deployment Status

The application is currently **not publicly deployed**.

Due to the limitations of free hosting tiers for realtime and WebSocket-based systems, 
this project prioritizes **clean architecture, system design, and documentation** 
over a degraded live deployment.

A demo video showcasing the complete functionality will be provided.


## 🎯 Project Purpose

This project was built as:

- ✅ A portfolio project
- ✅ A learning exercise to understand WebSockets and CRDTs
- ✅ An interview showcase demonstrating system design skills

The primary goal of Document Me is to deeply understand how real-time collaborative
systems like Google Docs work under the hood, rather than simply consuming libraries.

