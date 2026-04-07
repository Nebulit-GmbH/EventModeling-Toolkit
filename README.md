# Event Modeling Toolkit

A canvas-based tool for creating, visualizing, and generating code from **Event Modeling** diagrams. It runs as a standalone Next.js web application .

## What is Event Modeling?

Event Modeling is a method for designing information systems. It maps out how data changes over time using a sequence of:

- **Commands** — user intentions that trigger changes
- **Events** — facts that record what happened
- **Read Models** — projections of data for specific views
- **Aggregates** — domain entities enforcing business rules
- **Screens** — UI elements and their data requirements

This app provides an interactive canvas to model these elements, organize them into **Slices** (vertical feature slices) and **Bounded Contexts**, validate dependencies, and generate code.

## Overview

This Next.js application provides advanced Event Modeling capabilities on an interactive canvas (ReactFlow-based). It supports creating event-driven system models with various elements including events, commands, read models, and aggregates.

## Features

- **Event Modeling Elements**: Create and manage events, commands, read models, aggregates, and other Event Modeling components
- **AI Integration**: Built-in AI features for slice analysis and modeling assistance using OpenAI
- **Visual Design**: Interactive screen design tools and flow visualization
- **Code Generation**: Automated code generation from Event Modeling diagrams
- **Multi-language Support**: Internationalization support with JSON-based translations
- **Validation**: Model validation and linking verification tools


## Project Structure

```
src/
├── app/                    # Next.js app router pages
│   ├── api/               # API routes
│   ├── elements/          # Element management page
│   ├── flow/              # Flow visualization page
│   ├── modelui/           # Model UI page
│   └── prototype/         # Prototype and code generation
├── components/            # React components
│   ├── ai/               # AI integration components
│   ├── aicanvas/         # AI chat interface
│   ├── api/              # API utilities
│   ├── code/             # Code generation components
│   ├── i18n/             # Internationalization files
│   └── modelui/          # Model UI components
└── utils/                 # Utility functions
```

## Pages Structure

The application uses Next.js App Router with the following page structure:

### Main Pages

- **`/root`** - Landing page and main entry point for the application with tabbed interface:
  - **Model Tab** - Main model view for comprehensive Event Modeling management ([`ModelView`](src/components/ModelView.tsx) component)
  - **Board Tab** - Board setup and initialization tools ([`Starter`](src/components/Starter.tsx) component)
  - **Elements Tab** - Element management interface for creating/editing components ([`DataTable`](src/components/DataTable.tsx) component)
  - **Slices Tab** - Slice visualization and management ([`Slices`](src/components/Slices.tsx) component)
  - **Scenario Tab** - Scenario testing and validation ([`Scenario`](src/components/Scenario.tsx) component, requires authentication)
  - **Code Tab** - Code generation and AI-powered development tools ([`Code`](src/components/Code.tsx) component with [`ChatProvider`](src/components/aicanvas/ChatProvider.tsx), requires authentication)

- **`/elements`** - Element management interface for creating and editing Event Modeling components (uses [`DataTable`](src/components/DataTable.tsx) component)
- **`/flow`** - Flow visualization page for viewing event flows and system interactions ([`FlowData`](src/components/flow/FlowData.tsx) component)
- **`/modelui`** - Model user interface for comprehensive model viewing and management (uses [`ModelView`](src/components/ModelView.tsx) and related components)
- **`/screendesign`** - Screen design tools for UI/UX modeling ([`ScreenDesigner`](src/components/screendesigner/ScreenDesigner.tsx) component)
- **`/schemaeditor`** - Schema editor for defining data structures and field configurations ([`Fields`](src/app/schemaeditor/Fields.tsx) component)
- **`/prototype`** - Prototype page with code generation and dependency analysis tools (uses [`codeProvider.ts`](src/app/prototype/codeProvider.ts) and [`dependencyAnalyzer.ts`](src/app/prototype/dependencyAnalyzer.ts))
- **`/codegen-help`** - Help and documentation for code generation features

### API Routes

- **`/api/redirect`** - Handles OAuth redirects and authentication flows

### Special Features

## Key Components

- **ModelView**: Main application interface for Event Modeling
- **AIIntegration**: OpenAI-powered analysis and suggestions
- **ChatWindow**: Interactive AI chat for modeling assistance
- **Starter**: Initial setup and board creation tools
- **CodeGen**: Automated code generation from models

### ModelUI Components

The ModelUI subsystem provides specialized views for different aspects of Event Modeling:

- **[`AggregateView`](src/components/modelui/aggregates/AggregateView.tsx)** - Aggregate-centric view showing event dependencies and relationships within bounded contexts
- **[`Classic`](src/components/modelui/classic/Classic.tsx)** - Classic Event Modeling view with traditional table mappings and field relationships
- **[`DataTrail`](src/components/modelui/datatrail/DataTrail.tsx)** - Data flow visualization showing how information travels through the system
- **[`Overview`](src/components/modelui/overview/Overview.tsx)** - High-level overview of all model elements with filtering and search capabilities
- **[`Snapshots`](src/components/modelui/snapshots/Snapshots.tsx)** - Version control and comparison tool for tracking model changes over time
- **[`ModelElement`](src/components/modelui/overview/ModelElement.tsx)** - Reusable component for rendering individual model elements
- **[`SpecElement`](src/components/modelui/overview/SpecElement.tsx)** - Component for displaying specification elements and requirements

## Data Model

The application uses a comprehensive data model defined in [`src/components/model.tsx`](src/components/model.tsx) that represents all Event Modeling concepts:

### Core Element Types

- **`ElementType`** - Enumeration of all modeling elements (Command, Event, ReadModel, Aggregate, etc.)
- **`ElementData`** - Base class for all model elements with common properties (id, title, fields, dependencies)
- **`Field`** - Data structure definition with type, cardinality, mappings, and validation rules

### Event Modeling Elements

- **`Command`** - User intentions that trigger state changes
- **`Event`** - Facts that represent state changes in the system
- **`ReadModel`** - Projections of data optimized for specific read scenarios
- **`Aggregate`** - Domain entities that enforce business rules and consistency
- **`Screen`** - User interface elements and their data requirements
- **`ExternalData`** - External system integrations and data sources

### Organizational Elements

- **`Slice`** - Vertical feature slices containing related commands, events, and read models
- **`SliceGroup`** - Collections of related slices for higher-level organization
- **`Context`** - Bounded contexts that define boundaries between different parts of the system
- **`Actor`** - Roles or personas that interact with the system
- **`Spec`** - Specifications and acceptance criteria for features

### Supporting Types

- **`SliceType`** - Classification of slices (State Change, State View, Automation)
- **`SliceStatus`** - Workflow states for slice development (Planned, Assigned, Done, etc.)
- **`Context`** - Internal vs External system boundary classification
- **`Meta`** - Metadata for elements including positioning and visual properties
- **`FlowStep`** - Sequential steps in user workflows and processes

### Field System

- **`fieldtype`** - Data types (String, UUID, Boolean, Date, Custom, etc.)
- **`fieldCardinality`** - Single values vs Lists
- **`Field`** - Complete field definition with examples, mappings, and technical attributes

The model supports full Event Modeling methodology with proper relationships, dependencies, and metadata for visual representation.


## Opening Issues / Tickets

When reporting a bug or requesting a feature, please include the following information so it can be handled efficiently.

### Bug Reports

**Title format**: `[Bug] Short description of what went wrong`

Include:
- **What you did** — step-by-step reproduction (which tab, which element type, what action)
- **What you expected** — the intended behavior
- **What happened** — actual behavior, including any error messages or console output
- **Where on the canvas** — which area of the app (e.g., Elements tab, Slices view, Code generation, AI assistant)
- **Element types involved** — e.g., Command, Event, ReadModel, Aggregate, Slice

Example:
```
[Bug] Drag-dropping a Command onto the canvas does not create a link to the Aggregate

Steps:
1. Open canvas with an existing model
2. Drag a Command element near an Aggregate
3. Release

Expected: A connector is created between Command and Aggregate
Actual: No connector appears, no error shown

Element types: Command, Aggregate
Area: Main canvas
```

### Feature Requests / Bug Reports

**Title format**: `[Feature] Short description`

Include:
- **Problem being solved** — what workflow or use case is missing
- **Proposed behavior** — what you'd like the app to do
- **Element types or areas affected** — e.g., Slice management, Code generation, AI analysis
- **Priority/context** — is this blocking a modeling session? Nice-to-have?

### Understanding the App Areas

To help triage tickets, reference these areas:

| Area | Description |
|------|-------------|
| **Canvas** | Main ReactFlow canvas where elements are placed and connected |
| **Elements tab** | Table-based editor for creating/editing Commands, Events, etc. |
| **Model tab** | Overview of the full event model |
| **Slices tab** | Vertical feature slices grouping related elements |
| **Scenario tab** | Scenario/acceptance test authoring (requires auth) |
| **Code tab** | AI-powered code generation from the model (requires auth) |
| **Flow view** | Graph visualization of event flows |
| **Schema editor** | Field and data structure definitions |
| **Screen designer** | UI/UX mockup tools tied to the model |


