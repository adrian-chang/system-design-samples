### **System Design Question: Design a Distributed Real-Time Collaborative Whiteboard**

**Problem Statement:**
You are tasked with designing a real-time collaborative whiteboard application. This application allows multiple users to collaborate simultaneously on a shared canvas. Users can draw shapes, write text, erase content, and move objects around in real-time. The changes made by one user should be immediately visible to all other users collaborating on the same whiteboard.

**Requirements:**

1. **Functional Requirements:**
   - Multiple users can join the same whiteboard session.
   - Users can draw freehand lines, add shapes (e.g., circles, rectangles), and insert text.
   - Users can move, resize, and delete objects on the canvas.
   - Changes made by one user should be reflected in real-time for all other users.
   - Support for undo/redo functionality.
   - Users can save the state of the whiteboard and reload it later.
   - Optional: Support for chat or comments within the whiteboard session.

2. **Non-Functional Requirements:**
   - Low latency: Changes should be reflected in real-time with minimal delay.
   - High availability: The system should be resilient to failures.
   - Scalability: The system should support thousands of concurrent users across different whiteboard sessions.
   - Data consistency: Ensure that all users see the same state of the whiteboard at any given time.
   - Security: Ensure that only authorized users can access specific whiteboard sessions.

3. **Additional Considerations:**
   - How will you handle conflicts if two users modify the same object simultaneously?
   - How will you ensure smooth performance even when there are many objects on the canvas?
   - What happens if a user loses their internet connection? Should they be able to rejoin and continue where they left off?
   - How will you handle large whiteboards with complex drawings?

---

### **Steps to Work Through the Problem:**

1. **Clarify Requirements:**
   - Ask clarifying questions to understand the scope:
     - What is the expected number of concurrent users per whiteboard session?
     - Do we need to support offline mode or syncing after reconnection?
     - Should the whiteboard support versioning (e.g., saving snapshots of the canvas)?
     - What level of data consistency is required? (e.g., eventual consistency vs strong consistency)

2. **Define the API:**
   - Design the APIs for creating, joining, and interacting with the whiteboard.
     - Example: `POST /create` to create a new whiteboard session.
     - Example: `GET /join/{sessionId}` to join an existing session.
     - Example: `POST /update` to send updates (e.g., drawing actions) to the server.

3. **Design the Data Model:**
   - What data needs to be stored? (e.g., whiteboard session ID, user actions, object states, etc.)
   - How will you represent the state of the whiteboard? (e.g., JSON objects for shapes, lines, text)
   - How will you store the history of actions for undo/redo functionality?

4. **Real-Time Communication:**
   - How will you implement real-time communication between clients and the server?
     - Options: WebSockets, Server-Sent Events (SSE), or long polling.
   - How will you broadcast changes to all users in the session efficiently?

5. **Conflict Resolution:**
   - How will you handle conflicts when two users modify the same object simultaneously?
     - Options: Last-write-wins, operational transformation (OT), or Conflict-free Replicated Data Types (CRDTs).
   - How will you ensure that all users see a consistent view of the whiteboard?

6. **Scalability and Performance:**
   - How will you scale the system to handle thousands of concurrent users across different whiteboard sessions?
   - How will you optimize the rendering of complex drawings with many objects?
   - How will you reduce latency for real-time updates?

7. **Persistence and Recovery:**
   - How will you persist the state of the whiteboard so that users can reload it later?
   - How will you handle partial saves or crashes during a session?

8. **Security Considerations:**
   - How will you ensure that only authorized users can access specific whiteboard sessions?
   - How will you prevent unauthorized modifications to the whiteboard?
   - How will you protect sensitive data (e.g., chat messages or comments)?

9. **Edge Cases:**
   - What happens if a user loses their internet connection? Should they be able to rejoin and continue where they left off?
   - How will you handle very large whiteboards with thousands of objects?
   - How will you handle malicious users who try to spam the whiteboard with excessive actions?

---

### **Questions to Think About:**

- How will you ensure low latency for real-time updates while maintaining data consistency across multiple users?
- What is the best way to represent the state of the whiteboard in memory and in storage?
- How will you handle the trade-off between strong consistency and eventual consistency in a distributed system?
- How will you optimize the rendering of complex drawings with many objects, especially for users with slower devices or connections?
- How will you handle versioning or snapshots of the whiteboard state for users who want to revert to a previous version?
