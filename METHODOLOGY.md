# Chapter 3: Methodology

## 3.1 Introduction

This chapter presents the methodology used to design, implement, and evaluate SimuLab, a web-based virtual science laboratory for physics and chemistry experiments. The methodological goal was to produce a reproducible, educationally meaningful, and technically robust platform that supports interactive simulation, data capture, and experiment persistence.

The methodology follows an applied software engineering research approach, combining:

- iterative prototyping for interface and simulation behavior,
- model-driven implementation for physics and chemistry logic,
- API-centered persistence design for user and experiment data,
- and empirical validation through functional, numerical, and usability checks.

## 3.2 Research and Development Approach

### 3.2.1 Development Model

An iterative-incremental process was used. Each iteration delivered a complete vertical slice:

1. experiment logic (engine behavior),
2. interactive user interface,
3. data logging and visualization,
4. persistence and retrieval through API routes,
5. verification and refinement.

This approach reduced integration risk and allowed early feedback on simulation quality and educational usefulness.

### 3.2.2 Problem Decomposition

The project problem was decomposed into five engineering layers:

1. Presentation layer: experiment controls, canvas rendering, and chart views.
2. Simulation layer: real-time state updates for physics and chemistry models.
3. Data layer: time-series capture, analysis views, and export.
4. Service layer: API endpoints for authentication, students, experiments, and tutorials.
5. Persistence layer: MongoDB schema design and indexing.

## 3.3 System Design Methodology

### 3.3.1 Architecture Strategy

A client-side simulation and server-side persistence architecture was selected.

- Client-side simulation was chosen for responsive interaction and immediate visual feedback.
- Server-side persistence was chosen for multi-session continuity, report generation, and dashboard retrieval.

This separation allows high-frequency simulation loops to remain local while durable data management remains centralized.

### 3.3.2 Technology Selection Criteria

Tools were selected using four criteria: development speed, runtime performance, maintainability, and ecosystem maturity.

- Next.js with TypeScript for structured full-stack development.
- Matter.js and custom engines for deterministic or controlled simulation behavior.
- MongoDB with Mongoose for flexible experiment state storage.
- Recharts for near real-time visual analytics.
- Tailwind CSS for rapid and consistent component styling.

## 3.4 Data Modeling Methodology

### 3.4.1 Entity Design

Data entities were designed around educational workflows rather than only technical structure. Core entities include:

- users (roles, identity, institutional profile),
- experiments (state snapshots, category, status, report text),
- tutorials (experiment-linked instructional content),
- achievements (progress-related milestones).

### 3.4.2 Schema Strategy

A hybrid schema strategy was used:

- strongly defined fields for identity and filtering (e.g., category, status, role),
- flexible mixed state for simulation payloads that vary by experiment type,
- selective indexing for common query paths (owner/category/status/template flags).

This balances query performance with extensibility for new experiments.

## 3.5 Simulation Methodology

### 3.5.1 Numerical Update Model

Simulation updates follow discrete time-stepping with bounded delta time to reduce instability under variable frame rates.

Given state $S_t$ at time $t$, the next state is computed as:

$$
S_{t+\Delta t} = F(S_t, \Delta t, P)
$$

where $P$ are experiment parameters (mass, angle, gravity, etc.) and $\Delta t$ is clamped to prevent large jumps.

### 3.5.2 Physics Formulation

For projectile and free-fall behavior, classical kinematics were used with continuous capture of measured variables:

$$
x(t)=v_{0x}t, \qquad y(t)=h_0+v_{0y}t-\frac{1}{2}gt^2
$$

These analytical forms were used as educational references and compared to measured simulation traces.

### 3.5.3 Experiment Instrumentation

Each simulation step can be sampled into a time-series stream containing position, velocity, and derived quantities. Sampling interval was configured to provide a balance between smooth charts and manageable data size.

## 3.6 Implementation Procedure

Implementation was executed in phased order:

1. Base platform setup and routing.
2. Core simulation loop and experiment engines.
3. Workbench UI components and interactive controls.
4. Live charting and logger integration.
5. Export support (CSV and chart outputs).
6. API routes and MongoDB model integration.
7. Tutorial and student management flows.
8. Documentation and verification artifacts.

Each phase ended with local integration checks before moving to the next phase.

## 3.7 Validation and Evaluation Methodology

### 3.7.1 Functional Validation

Functional validation used scenario-based tests:

- launching and controlling experiments,
- pausing/resetting simulation state,
- saving and retrieving experiment records,
- tutorial retrieval and rendering,
- student CRUD and authentication paths.

### 3.7.2 Numerical and Behavioral Validation

Simulation credibility was checked by comparing expected qualitative behavior and, where applicable, analytic trends:

- monotonic acceleration under gravity,
- expected trajectory shape for projectile motion,
- conservation-oriented behavior in collision scenarios,
- stable response under different frame rates.

### 3.7.3 Data and Output Validation

Validation also covered:

- chart consistency with logged values,
- export file integrity,
- correct persistence and reload of experiment state,
- schema-conformant API payloads.

## 3.8 Reliability and Quality Controls

Quality controls included:

- TypeScript type checking to reduce interface mismatch,
- modular separation of engine, UI, and API concerns,
- controlled update intervals for performance stability,
- defensive validation in API routes for required fields,
- incremental documentation of completed modules and tests.

## 3.9 Ethical and Educational Considerations

The platform was designed for educational enhancement rather than replacing physical labs. Methodologically, this implies:

- clear instructional context through tutorials,
- transparent formulas and measured values,
- reproducible student workflows,
- avoidance of overstated physical realism claims.

## 3.10 Limitations of Method

The method has known limits:

- browser-based simulation precision is bounded by frame timing and floating-point behavior,
- simplified models may omit secondary effects (e.g., drag, measurement noise),
- performance can vary across device classes,
- some educational outcomes still depend on instructor guidance.

## 3.11 Reproducibility

The project supports reproducibility through:

- deterministic parameterized initialization for many experiments,
- version-controlled source and documentation,
- scripted data seeding,
- explicit setup and run instructions.

## 3.12 Summary

The adopted methodology combines iterative development, model-based simulation, API-driven persistence, and layered validation. This provides a practical and academically defensible path for building an interactive virtual laboratory that is technically maintainable and pedagogically useful.
