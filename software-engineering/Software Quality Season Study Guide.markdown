# Software Quality

## Section 1: Understanding Software Quality Attributes
- **What Are Quality Attributes?**
  - Also called "architectural characteristics" or "ilities" (e.g., scalability, availability).
  - Define how well a system performs non-functional requirements (e.g., speed, reliability).
  - Drive architectural decisions to ensure the system meets user needs.
- **Key Quality Attributes** (from eBay example, p.101):
  - **Scalability**: Ability to handle increased load (e.g., more users registering for courses).
  - **Availability**: System stays operational, even during failures (e.g., grade system accessible during exams).
  - **Manageability**: Ease of monitoring and maintaining the system.
  - **Cost**: Minimizing resource expenses (e.g., using affordable servers).
- **Why It Matters**: Quality attributes guide trade-offs in design (e.g., performance vs. security).
- **Example**: In a student system, high scalability ensures the system handles thousands of course registrations during peak times without crashing.

**Visual: Quality Attributes Trade-Off Table**

| Attribute     | Benefit                              | Trade-Off                         |
|---------------|--------------------------------------|-----------------------------------|
| Scalability   | Handles more users                   | Higher infrastructure cost        |
| Availability  | System stays up during failures      | Complex redundancy needed         |
| Manageability | Easy to monitor/maintain             | May limit flexibility             |
| Cost          | Cheaper to run                       | May sacrifice performance         |

**Exam Tip**: Be ready to define quality attributes and give examples. For scenario questions, identify which attribute is prioritized (e.g., scalability for a registration spike).

## Section 2: Architectural Decisions and Quality
- **What Are Architectural Decisions?**
  - Choices that shape the system’s structure and behavior (e.g., choosing microservices vs. monolithic).
  - Impact quality attributes like performance, maintainability, or extensibility.
- **Key Concepts** (p.93, p.107):
  - **Trade-Offs**: Every decision has pros and cons (e.g., microservices improve scalability but increase complexity).
  - **Documenting “Why”**: Record reasons for decisions to avoid blind changes later.
  - **Architecture Decision Records (ADRs)**: Lightweight format to document decisions (Title, Status, Context, Decision, Reasons, Consequences, Compliance).
- **Example**: For a student system, choosing a single shared database (p.92):
  - **Pros**: Consistent student data, low query cost.
  - **Cons**: Larger database, higher operational load.
  - **ADR**: Document why a shared database was chosen for data consistency in course registration.

**Visual: ADR Flow (Mermaid Diagram)**

[![](https://mermaid.ink/img/pako:eNo9kctuwjAQRX_FmnVACQl5LSqVBCoWdNFWXdRhYSUDWBA79UOiRfx7HQP1yqNz7x175gKt7BBKaMReseFAPupGEHee6bpDYfjuh6y1trglk8kTWdAad1wgqaQweDbbm3jhYUU37IikxpZrLsWdVZ7VtJat7V0ieUOmpdB3XHu8pK_S-FSN3xZFiw--9HxFl0JbNSr64cSZE9z5yvMX-m6kw1yQT1Rjd_9CJU9bCGCveAfljp00BtCj6tlYw2VMaMAcsMcGSnftmDo2bhRXZxqY-JKyh9Io62xK2v3hUdihYwZrztzM-v9khaJDVUkrDJRxVPgMKC9wduUsnKZZGEd5GsbzaJ4G8DOKpsUsz_I4idIsycMkuwbw67uG0yKeF3kRZmkRp1GSOgd23P1yc1uY39v1D0L4iUU?type=png)](https://mermaid.live/edit#pako:eNo9kctuwjAQRX_FmnVACQl5LSqVBCoWdNFWXdRhYSUDWBA79UOiRfx7HQP1yqNz7x175gKt7BBKaMReseFAPupGEHee6bpDYfjuh6y1trglk8kTWdAad1wgqaQweDbbm3jhYUU37IikxpZrLsWdVZ7VtJat7V0ieUOmpdB3XHu8pK_S-FSN3xZFiw--9HxFl0JbNSr64cSZE9z5yvMX-m6kw1yQT1Rjd_9CJU9bCGCveAfljp00BtCj6tlYw2VMaMAcsMcGSnftmDo2bhRXZxqY-JKyh9Io62xK2v3hUdihYwZrztzM-v9khaJDVUkrDJRxVPgMKC9wduUsnKZZGEd5GsbzaJ4G8DOKpsUsz_I4idIsycMkuwbw67uG0yKeF3kRZmkRp1GSOgd23P1yc1uY39v1D0L4iUU)

**Exam Tip**: Expect questions on trade-offs (e.g., “Why choose a shared database?”). Use ADRs to structure answers: context, decision, pros/cons.

## Section 3: Architectural Strategies for Quality
- **What Are Architectural Strategies?**
  - Design principles to achieve quality attributes (p.101-102).
  - Example: eBay’s strategies for scalability and availability.
- **Key Strategies**:
  - **Partitioning (Sharding)**: Split data or load into smaller parts (e.g., shard student database by department).
    - **Impact**: Improves scalability, availability; reduces cost.
  - **Automation**: Auto-configure system for load changes (e.g., auto-scale servers during registration).
    - **Impact**: Enhances manageability, resilience.
- **Example**: In a student system, partition the grade database by academic year to improve query speed and scalability.

**Visual: Gantt Chart for Partitioning Implementation**

```markdown
| Task                     | Week 1 | Week 2 | Week 3 | Week 4 |
|--------------------------|--------|--------|--------|--------|
| Analyze Data Needs       | ███    |        |        |        |
| Design Shard Strategy    |        | ███    |        |        |
| Implement Sharding       |        |        | ███    |        |
| Test Scalability         |        |        |        | ███    |
```

**Exam Tip**: Be prepared to explain how a strategy (e.g., partitioning) improves specific quality attributes. Use examples like sharding student data.

## Section 4: Documenting Architecture for Quality
- **Why Document?**
  - Communicates decisions to stakeholders (p.103).
  - Ensures quality attributes are maintained (e.g., scalability through load balancing).
- **Key Documentation Types** (p.107-108):
  - **Quality Attribute Requirements Document**: Lists stakeholders, quality needs (e.g., performance for grade queries).
  - **Architecture Document**: Includes views (Component-Connector, Module, Allocation) and explains decisions.
  - **ADRs**: Capture specific decisions (e.g., REST vs. RPC for student API).
- **Example**: For a student system, document the Component-Connector view showing how the registration app connects to the database via a load balancer for scalability.

**Visual: Component-Connector View (ASCII)**

```
[Browser] --> [Load Balancer] --> [Registration App]
                                    |
                                  [Database]
```

**Exam Tip**: For diagram questions, sketch simple views (e.g., Component-Connector) and label quality attributes (e.g., “Load Balancer for Scalability”). Practice ADRs for decision questions.

## Section 5: Quality in Agile and XP
- **Quality in Agile** (p.19-20):
  - Emphasizes working software over documentation, but quality is non-negotiable.
  - Uses data (e.g., burn-down charts) to track progress and ensure quality.
- **Extreme Programming (XP) Practices** (p.20):
  - **Test-Driven Development (TDD)**: Write tests first to ensure code quality.
  - **Continuous Integration**: Frequent integration to catch issues early.
  - **Pair Programming**: Improves code quality through collaboration.
- **Example**: In a student system, use TDD to write tests for the course registration API to ensure it handles invalid inputs correctly.

**Visual: TDD Flow (Mermaid)**

[![](https://mermaid.ink/img/pako:eNpVkE1rwzAMhv9K0KmDNNh14iQ-DNqkuw3GKAzW9GBqNQlrPnAc2Bby3-e6LWX2xXrfR5KlCY6dQhBQtP9vqWVfebu8aD171vsPXRv0djiYg7dcPnubxYusz8PT1d84LbtRmS15uBqZM_LFmxwGvNO5E7f7dzzJo-n0jd06eQ0-lLpWIE7yPKAPDepGXmKYLlwBpsIGCxD2qaT-KuzfZ5vUy_az6xoQRo82TXdjWd2DsVfSYF5LO9aDwFahzrqxNSBo6CqAmOAbBFuRgMeE0YQTFtGI-_BjVRqkqyROWEh5HCYkjGcffl1PEqQsSpOUUhJGnHGe-ICqtsO9Xvfr1jz_AbTObF4?type=png)](https://mermaid.live/edit#pako:eNpVkE1rwzAMhv9K0KmDNNh14iQ-DNqkuw3GKAzW9GBqNQlrPnAc2Bby3-e6LWX2xXrfR5KlCY6dQhBQtP9vqWVfebu8aD171vsPXRv0djiYg7dcPnubxYusz8PT1d84LbtRmS15uBqZM_LFmxwGvNO5E7f7dzzJo-n0jd06eQ0-lLpWIE7yPKAPDepGXmKYLlwBpsIGCxD2qaT-KuzfZ5vUy_az6xoQRo82TXdjWd2DsVfSYF5LO9aDwFahzrqxNSBo6CqAmOAbBFuRgMeE0YQTFtGI-_BjVRqkqyROWEh5HCYkjGcffl1PEqQsSpOUUhJGnHGe-ICqtsO9Xvfr1jz_AbTObF4)

**Exam Tip**: Know XP practices like TDD and their impact on quality. For Agile questions, highlight how working software ensures quality over extensive documents.

## Example: Student System Quality
- **Scenario**: Building a course registration system using Spring Boot.
- **Quality Focus**:
  - **Scalability**: Use sharding to split student data by department.
  - **Availability**: Deploy multiple app instances behind a load balancer.
  - **Code Quality**: Use TDD for REST endpoints (e.g., `/register`).
- **ADR Example**:
  - **Title**: Use REST for Registration API.
  - **Context**: Need fast, scalable API for student registration.
  - **Decision**: Use REST with Spring Boot.
  - **Reasons**: Stateless, scalable, widely supported.
  - **Consequences**: Higher latency than RPC but easier to scale.
  - **Compliance**: Code reviews to ensure REST standards.

**Code Snippet (TDD for Registration API)**

```java
@Test
public void testRegisterCourse() {
    CourseRegistrationRequest request = new CourseRegistrationRequest("CS101", "S123");
    ResponseEntity<String> response = restTemplate.postForEntity("/register", request, String.class);
    assertEquals(HttpStatus.OK, response.getStatusCode());
    assertEquals("Registered", response.getBody());
}
```

## Exam Tips Summary
1. **Definitions**: Memorize key terms (quality attributes, ADRs, partitioning).
2. **Comparisons**: Practice tables comparing strategies (e.g., partitioning vs. automation) or architectures (e.g., shared vs. separate database).
3. **Scenarios**: Apply concepts to a student system (e.g., “How to ensure scalability?”).
4. **Diagrams**: Sketch Component-Connector or flowcharts for architecture questions.
5. **ADRs**: Use the ADR format for decision-based questions (Context, Decision, Reasons).
6. **Time Management**: Answer short questions first, then tackle scenarios/diagrams.
7. **AI-Generated Exam**: Expect clear, structured questions. Focus on concise answers with examples.

**Study Plan (Tonight)**:
- Review each section (30 min).
- Practice one diagram (e.g., Component-Connector) and one ADR (15 min).
- Skim example scenario and code (10 min).
- Sleep early to stay sharp!
