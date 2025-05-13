# Process Evolution

## Section 2.1: Before Software Engineering (1950s-1960s)
- **Overview** (p.1-2):
  - Software development mirrored hardware engineering; no clear distinction.
  - Sequential processes like the SAGE project (radar system) resembled early Waterfall.
- **Key Points**:
  - **1950s**: Software treated as hardware; sequential steps (Operational Plan → Specifications → Coding → Testing).
  - **1960s**: High demand led to less formality; "Cowboy Programmers" rejected rigid processes, influenced by counter-culture.
  - Software’s ease of change (e.g., punch cards) reduced upfront planning compared to hardware.
- **Example**: In a student system, 1960s developers might code a grade calculator without specs, updating via punch cards.

**Visual: 1950s Process Flow (Mermaid)**

```mermaid
graph TD
    A[Operational Plan] --> B[Machine Spec]
    B --> C[Program Spec]
    C --> D[Coding Spec]
    D --> E[Coding]
    E --> F[Testing]
```

**Exam Tip**: Know the sequential nature of 1950s processes and the 1960s shift to less formality. Be ready to explain “Cowboy Programmers.”

## Section 2.2.1: Waterfall Model
- **Overview** (p.3-4):
  - Formalized sequential process with distinct phases; no backtracking initially.
  - Used in mission-critical systems (e.g., DoD-STD-2167 standard).
- **Key Phases**:
  - System Requirements → Software Requirements → Analysis → Design → Coding → Testing → Installation.
  - Later versions allowed informal revisits to earlier phases.
- **Pros**: Clear structure, good for accountability in public-funded projects.
- **Cons**: Late integration, outdated documentation, high risk until end.
- **Example**: For a student system, Waterfall would define all course registration requirements before coding, delaying feedback.

**Visual: Waterfall Phases Table**

| Phase              | Task Example                     | Output                     |
|--------------------|----------------------------------|----------------------------|
| System Requirements| Define registration system needs | System specs              |
| Design             | Plan database schema            | Design documents          |
| Coding             | Build REST API                  | Codebase                  |
| Testing            | Test registration endpoint      | Test reports              |

**Exam Tip**: List Waterfall phases and their pros/cons. For scenarios, note its suitability for fixed-requirement projects.

## Section 2.2.2: Waterfall Planning and Issues
- **Overview** (p.6-8):
  - Emphasizes planning (e.g., Work Breakdown Structure, Gantt charts).
  - Issues: Inaccurate long-term plans, unrealistic progress tracking.
- **Key Points**:
  - **WBS**: Breaks project into tasks (e.g., requirements, coding).
  - **Gantt Charts**: Show task timelines but lose accuracy due to unknowns.
  - Problems: Late integration, high pressure near deadlines, adversarial client relations.
- **Example**: A Gantt chart for a student system might overestimate coding time, causing delays when bugs arise.

**Visual: Gantt Chart for Student System**

```markdown
| Task                | Week 1 | Week 2 | Week 3 | Week 4 |
|---------------------|--------|--------|--------|--------|
| Requirements        | ███    |        |        |        |
| Design              |        | ███    |        |        |
| Coding              |        |        | ███    |        |
| Testing             |        |        |        | ███    |
```

**Exam Tip**: Explain why Gantt charts fail in software (e.g., unknowns). Critique Waterfall’s late integration for scenario questions.

## Section 2.3.1: Iterative and Incremental Development
- **Overview** (p.9-12):
  - Response to Waterfall’s issues; uses short, time-boxed iterations.
  - Delivers working software increments for frequent feedback.
- **Key Points**:
  - **Time-Boxed Iterations**: Fixed duration (e.g., 2 weeks); no deadline extensions.
  - **Feedback Loop**: Investigate missed deadlines to improve (e.g., overestimation, poor code quality).
  - Addresses unknowns early, unlike Waterfall’s late risk discovery.
- **Example**: In a student system, deliver a basic course registration feature in 2 weeks, then refine based on feedback.

**Visual: Iterative Cycle (Mermaid)**

```mermaid
graph TD
    A[Plan Iteration] --> B[Develop Increment]
    B --> C[Deploy & Test]
    C --> D[Get Feedback]
    D --> A
```

**Exam Tip**: Compare Iterative vs. Waterfall (e.g., early feedback vs. late integration). Know causes of missed iterations (e.g., dirty code).

## Section 2.3.2: Rational Unified Process (RUP)
- **Overview** (p.13-15):
  - Iterative-incremental framework with four phases; tailorable for projects.
- **RUP Phases**:
  - **Inception**: Define scope, assess risks (e.g., competitor systems).
  - **Elaboration**: Establish architecture, reduce technical risks.
  - **Construction**: Build system iteratively (e.g., add features).
  - **Transition**: Deploy to customer, user training.
- **Key Features**: Risk-driven, focuses on executable architecture.
- **Example**: For a student system, Elaboration defines a REST-based architecture for scalability.

**Visual: RUP Phases Table**

| Phase        | Focus                          | Example Deliverable          |
|--------------|--------------------------------|------------------------------|
| Inception    | Scope, business risks         | Use case list               |
| Elaboration  | Architecture, technical risks | System design               |
| Construction | Build features                | Working registration API    |
| Transition   | Deployment, training          | User manual                 |

**Exam Tip**: List RUP phases and their goals. Explain how it balances planning and iteration for process comparison questions.

## Section 2.4: Introduction to Agile
- **Overview** (p.17-18):
  - Emphasizes flexibility, collaboration, and working software.
  - Based on Agile Manifesto’s four values.
- **Agile Manifesto Values**:
  - Individuals and interactions > processes and tools.
  - Working software > comprehensive documentation.
  - Customer collaboration > contract negotiation.
  - Responding to change > following a plan.
- **Key Points**: Uses data (e.g., burn-down charts) for progress; manages scope to meet deadlines.
- **Example**: In a student system, deliver a minimal registration feature and adjust scope based on user feedback.

**Visual: Agile Feedback Loop (Mermaid)**

```mermaid
graph TD
    A[Customer Feedback] --> B[Adjust Scope]
    B --> C[Develop Feature]
    C --> D[Deliver Software]
    D --> A
```

**Exam Tip**: Memorize Agile Manifesto values. Highlight how Agile prioritizes working software in short-answer or scenario questions.

## Section 2.5: Extreme Programming (XP)
- **Overview** (p.19-20):
  - Agile methodology with practices to ensure quality and collaboration.
- **Key XP Practices**:
  - **Planning Game**: Prioritize high-value features.
  - **Test-Driven Development (TDD)**: Write tests before code.
  - **Pair Programming**: Two developers code together.
  - **Continuous Integration**: Frequent code integration.
- **Promises**: Programmers focus on important tasks; customers see frequent progress.
- **Example**: Use TDD for a student system’s `/register` endpoint to ensure quality.

**Visual: TDD Process (Mermaid)**

```mermaid
graph TD
    A[Write Test] --> B[Run Test: Fails]
    B --> C[Write Code]
    C --> D[Run Test: Passes]
    D --> E[Refactor]
    E --> A
```

**Code Snippet (TDD for Registration)**

```java
@Test
public void testRegisterCourse() {
    CourseRequest request = new CourseRequest("CS101", "S123");
    ResponseEntity<String> response = restTemplate.postForEntity("/register", request, String.class);
    assertEquals(HttpStatus.OK, response.getStatusCode());
    assertEquals("Registered", response.getBody());
}
```

**Exam Tip**: List XP practices and their benefits (e.g., TDD for quality). Use examples like TDD for API endpoints in practical questions.

## Section 2.6: Scrum Intro
- **Overview** (p.21-22, assumed based on context):
  - Agile framework focusing on iterative delivery, team collaboration, and defined roles.
  - Uses time-boxed sprints (typically 2-4 weeks) to deliver increments.
- **Key Elements**:
  - **Roles**: Product Owner (defines priorities), Scrum Master (facilitates process), Team (delivers work).
  - **Artifacts**: Product Backlog (prioritized features), Sprint Backlog (tasks for sprint), Increment (delivered software).
  - **Events**: Sprint Planning, Daily Scrum (stand-up), Sprint Review, Sprint Retrospective.
- **Pros**: Clear roles, frequent delivery, adaptability to change.
- **Cons**: Requires discipline, can be chaotic without experienced Scrum Master.
- **Example**: In a student system, a 2-week sprint delivers a course registration API, with daily stand-ups to track progress.

**Visual: Scrum Process Flow (Mermaid)**

```mermaid
graph TD
    A[Product Backlog] --> B[Sprint Planning]
    B --> C[Sprint Backlog]
    C --> D[Daily Scrum]
    D --> E[Develop Increment]
    E --> F[Sprint Review]
    F --> G[Sprint Retrospective]
    G --> A
```

**Exam Tip**: Know Scrum roles, artifacts, and events. For questions, explain how Scrum ensures frequent delivery (e.g., via sprints).

## Section 2.7: Agile Culture
- **Overview** (p.23-24, assumed based on context):
  - Focuses on fostering a mindset that supports Agile values: collaboration, trust, and continuous improvement.
  - Encourages self-organizing teams and open communication.
- **Key Points**:
  - **Self-Organizing Teams**: Teams decide how to complete work, boosting ownership.
  - **Transparency**: Share progress (e.g., via burn-down charts) to build trust.
  - **Continuous Improvement**: Reflect on processes (e.g., retrospectives) to improve.
  - Aligns with Agile Manifesto’s emphasis on individuals and interactions.
- **Example**: In a student system project, the team holds retrospectives to improve sprint planning, ensuring better estimation for registration features.

**Visual: Agile Culture Principles Table**

| Principle              | Description                          | Example in Student System         |
|------------------------|--------------------------------------|-----------------------------------|
| Self-Organization      | Team decides tasks and methods       | Team assigns API tasks            |
| Transparency           | Open progress sharing                | Daily stand-up updates            |
| Continuous Improvement | Reflect and improve processes        | Retrospective on sprint delays    |

**Exam Tip**: Explain how Agile culture supports delivery (e.g., self-organization improves efficiency). Be ready to link to Agile Manifesto values.

## Example: Student System Process
- **Scenario**: Building a course registration system with Spring Boot.
- **Process Choice**:
  - **Scrum/XP**: Use 2-week sprints, TDD, and daily stand-ups.
  - **Why**: Frequent feedback from students, adaptable to changing requirements.
- **Implementation**:
  - Sprint 1: Basic `/register` endpoint with TDD.
  - Use Kafka for event-driven notifications (e.g., to finance system).
  - Hold retrospectives to refine sprint planning.
- **Agile Culture**: Team self-assigns tasks, shares progress in stand-ups.

## Exam Tips Summary
1. **Definitions**: Know key terms (e.g., Waterfall phases, Scrum roles, Agile culture principles).
2. **Comparisons**: Use tables to compare methodologies (e.g., Waterfall vs. Scrum).
3. **Scenarios**: Apply processes to a student system (e.g., “Why use Scrum?”).
4. **Diagrams**: Sketch flows (e.g., Scrum process, TDD cycle).
5. **Code**: Explain TDD or REST snippets for XP questions.
6. **Time Management**: Answer definitions first, then comparisons/scenarios.
7. **AI-Generated Exam**: Expect clear questions on pros/cons or process selection. Use examples to stand out.

**Study Plan (Tonight)**:
- Review each section (45 min).
- Practice one diagram (e.g., Scrum flow) and one comparison table (15 min).
- Test the TDD snippet in a Spring Boot project (10 min).
- Rest to stay sharp!
