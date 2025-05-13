# Software Architecture

## Section 1: Architectural Styles
- **What Are Architectural Styles?** (p.94-95)
  - Reusable packages of design decisions and constraints that shape system structure.
  - Influence quality attributes (e.g., scalability, reusability).
- **Key Styles**:
  - **Pipe and Filter** (p.95-96):
    - Components (filters) process data in a chain, connected by pipes.
    - Common in neuroimaging; high reusability, low fault tolerance.
    - Example: Process student grade data (filter 1: clean data, filter 2: calculate GPA).
  - **Service-Based Architecture** (p.97):
    - Breaks system into components with a shared UI and database.
    - High deployability, fault tolerance.
  - **Microservice Architecture** (p.98):
    - Small, independent services with own databases.
    - High evolutionary nature, but complex and costly.
- **Example**: In a student system, use microservices for course registration and grade management to scale independently.

**Visual: Styles Comparison Table**

| Style                | Pros                              | Cons                              |
|----------------------|-----------------------------------|-----------------------------------|
| Pipe and Filter      | High reusability, simple          | Low fault tolerance, batch-oriented |
| Service-Based        | High deployability, modular       | Shared DB limits evolution        |
| Microservices        | Evolutionary, scalable            | High cost, complex management     |

**Exam Tip**: Be ready to define styles and compare their trade-offs. For scenarios, suggest a style (e.g., microservices for scalability) and justify it.

## Section 2: Architectural Patterns
- **What Are Architectural Patterns?** (p.98-99)
  - Solutions to common problems, with smaller scope than styles.
  - Example: **Publish-Subscribe (Pub/Sub)**:
    - Publishers send events to a topic; subscribers receive them.
    - Decouples components, improves extensibility.
- **Pub/Sub Benefits**:
  - Decoupling, asynchronous communication, high testability.
- **Pub/Sub Challenges**:
  - Message queue reliability, security, message ordering.
- **Example**: In a student system, publish a “course registered” event to notify the finance and dormitory systems.

**Visual: Pub/Sub Flow (Mermaid Diagram)**

```mermaid
graph TD
    A[Course Registration] -->|Publish| B[Topic: Course Events]
    B -->|Subscribe| C[Finance System]
    B -->|Subscribe| D[Dormitory System]
```

**Exam Tip**: Know the difference between styles and patterns. For Pub/Sub questions, list benefits (e.g., decoupling) and concerns (e.g., message loss).

## Section 3: Architectural Principles and Strategies
- **What Are Architectural Principles?** (p.101)
  - Guidelines to achieve quality attributes (e.g., scalability, availability).
- **Key Strategies** (eBay example, p.101-102):
  - **Partitioning**: Split data or load (e.g., shard student database by department).
    - Improves scalability, availability.
  - **Automation**: Auto-scale resources for load changes.
    - Enhances manageability.
- **Example**: Shard the student system’s database by faculty to handle high registration traffic.

**Visual: Gantt Chart for Partitioning**

```markdown
| Task                     | Week 1 | Week 2 | Week 3 | Week 4 |
|--------------------------|--------|--------|--------|--------|
| Define Sharding Strategy | ███    |        |        |        |
| Implement Shards         |        | ███    |        |        |
| Test Scalability         |        |        | ███    |        |
| Deploy Shards            |        |        |        | ███    |
```

**Exam Tip**: Explain how strategies like partitioning improve quality attributes. Use examples like sharding for scalability questions.

## Section 4: Modeling and Documenting Architecture
- **Why Model Architecture?** (p.103)
  - Communicates decisions to stakeholders (developers, testers).
  - Captures structures (components, modules) not visible in code.
- **Key Views** (p.104-105):
  - **Component-Connector**: Shows runtime components and connections (e.g., load balancer to app).
  - **Module**: Shows code structure and dependencies (e.g., Domain Logic module).
  - **Allocation**: Maps components to physical nodes (e.g., servers).
- **Architecture Decision Records (ADRs)** (p.106):
  - Document decisions (e.g., REST vs. RPC) with context, reasons, consequences.
- **Example**: For a student system, model a Component-Connector view with a load balancer for scalability.

**Visual: Component-Connector View (ASCII)**

```
[Browser] --> [Load Balancer] --> [Course App]
                                    |
                                  [Database]
```

**Exam Tip**: Practice sketching views (e.g., Component-Connector) and writing ADRs. For questions, label diagrams with quality attributes (e.g., “Load Balancer for Scalability”).

## Section 5: Architecture in Development Processes
- **Architecture’s Role** (p.109-110):
  - **RUP**: Designs architecture in Elaboration phase to reduce change costs.
  - **Agile**: Spreads decisions across iterations, focusing on executable architecture.
- **Executable Architecture/Walking Skeleton** (p.110):
  - A minimal, runnable system (e.g., basic course registration with UI and DB).
  - Tests architectural decisions early (e.g., REST API scalability).
- **Example**: Build a walking skeleton for a student system with a REST endpoint for course registration using Spring Boot.

**Visual: Walking Skeleton Flow (Mermaid)**

```mermaid
graph TD
    A[Browser] --> B[REST API: /register]
    B --> C[Course Service]
    C --> D[Database]
```

**Code Snippet (Spring Boot REST Endpoint)**

```java
@RestController
public class CourseController {
    @PostMapping("/register")
    public ResponseEntity<String> registerCourse(@RequestBody CourseRequest request) {
        // Simplified logic
        return ResponseEntity.ok("Course registered");
    }
}
```

**Exam Tip**: Compare RUP vs. Agile for architecture timing. For walking skeleton questions, describe a minimal system and its purpose (e.g., test scalability).

## Example: Student System Architecture
- **Scenario**: Designing a course registration system with Spring Boot.
- **Architecture**:
  - **Style**: Microservices for scalability (separate course and grade services).
  - **Pattern**: Pub/Sub to notify finance system of registrations.
  - **Strategy**: Partition database by department.
  - **Model**: Component-Connector view with load balancer.
  - **Process**: Use Agile with a walking skeleton (basic `/register` endpoint).
- **ADR Example**:
  - **Title**: Use Microservices for Course System.
  - **Context**: Need scalable registration system.
  - **Decision**: Deploy course and grade services separately.
  - **Reasons**: Independent scaling, fault isolation.
  - **Consequences**: Higher management cost, complex deployment.
  - **Compliance**: Monitor services with Docker.

## Exam Tips Summary
1. **Definitions**: Memorize styles (e.g., Pipe and Filter), patterns (e.g., Pub/Sub), and views (e.g., Component-Connector).
2. **Comparisons**: Use tables to compare styles or strategies (e.g., microservices vs. service-based).
3. **Scenarios**: Apply architecture to a student system (e.g., “How to scale registration?”).
4. **Diagrams**: Sketch Component-Connector or Pub/Sub flows, labeling quality attributes.
5. **ADRs**: Structure answers with context, decision, and trade-offs.
6. **Time Management**: Tackle definitions first, then diagrams/scenarios.
7. **AI-Generated Exam**: Expect clear questions on trade-offs or practical applications. Use examples to stand out.

**Study Plan (Tonight)**:
- Review each section (30 min).
- Practice one diagram (e.g., Component-Connector) and one ADR (15 min).
- Test the code snippet in a Spring Boot project (10 min).
- Rest to stay focused!
