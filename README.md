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


## 🧠 Project Evolution & Design Journey

This project started with a simple goal: to build a high-performance notepad application where data could be stored, retrieved, and updated efficiently. As development progressed, the complexity of the problem space became more apparent, and the project gradually evolved into a collaborative document editor similar to Google Docs.

---

## Initial Approach

The initial design was based on a row-level storage model:

- Each line in the editor was mapped directly to a row in the database
- Data retrieval was planned using pagination for efficient rendering
- Updates were performed at the row level

### Challenges

#### 1. Inefficient Updates

Even a small change, such as editing a single word, required updating the entire row in the database. This resulted in unnecessary write operations and reduced efficiency.

---

#### 2. Row Ordering Issues

Handling insertion of new rows introduced ordering problems:

- Inserting between rows required reordering existing rows
- Adding a new row at the top changed the index of all existing rows

##### Attempted Solution: Lexicographic Ordering

To address this, a lexicographic indexing approach was implemented:

- Example:
  - Existing rows: `1`, `2`
  - Insert between → `1.5`
  - Insert at top → `0.5`

##### Limitations

- Index values became increasingly complex over time
- Precision and maintainability issues arose with frequent insertions

---

#### 3. Styling and Markup Complexity

Handling rich text formatting was another major challenge.

##### Initial Design

- A separate table was created to store styling information
- Each style entry referenced a corresponding row

##### Problems

- Difficult to support partial styling (e.g., styling a single word or character)
- Updating styles became complex and error-prone
- Increased difficulty in maintaining consistency between content and styles

---

## Rethinking the Architecture

After encountering multiple limitations, it became clear that building a scalable and efficient document editor required a different approach. The initial custom design was not sufficient to handle the complexities of real-world editing and collaboration.

---

## Key Features

- Rich text editing with fine-grained styling  
- Efficient data handling and updates  
- Real-time multi-user collaboration  
- Conflict-free synchronization using CRDTs  
- Improved scalability compared to the initial design  

---

## Key Learnings

- Simple data models can become bottlenecks as complexity grows  
- Managing ordering, updates, and styling in document systems is non-trivial  
- CRDT-based approaches provide a reliable solution for collaboration  
- Using established tools and frameworks significantly reduces complexity  

---

## Conclusion

What began as a simple notepad application evolved into a collaborative and scalable document editing system. This journey involved rethinking core design decisions, addressing architectural challenges, and adopting modern technologies to build a more robust solution.



