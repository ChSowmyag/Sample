# Categorized UML Documentation Reference

This document provides a single consolidated view of all UML diagrams for the **AR Car Showcase** project, organized by category as requested.

---

## 🏗️ 1. Structural Diagrams

_Focus on the static structure and components of the system._

### System Architecture

![Architecture Diagram](./Structural/architecture_diagram.md)

> High-level overview of the React Native frontend, Viro engine, and multi-service backend.

### Component Structure

![Component Diagram](./Structural/component_diagram.md)

> Modular breakdown of navigation, state management, and service layers.

### Data & Class Structure

![Class Diagram](./Structural/class_diagram_core.md)

> Definition of core TypeScript entities, context providers, and service modules.

---

## 🚦 2. Behavioral Diagrams

_Focus on the dynamic functionality and user interactions._

### Use Case

![Use Case Diagram](./Behavioral/use_case_diagram.md)

> Primary user actions and system boundaries.

### App State Machine

![State Diagram](./Behavioral/state_diagram.md)

> Navigation states and transitions between different viewer modes.

### User Journey (Activity)

![Activity Diagram](./Behavioral/activity_diagram.md)

> Step-by-step logic of the typical user experience from launch to AR.

---

## 🔄 3. Interaction Diagrams

_Focus on the chronological exchange of messages between objects._

### Authentication Flow

![Sequence Auth](./Interactions/sequence_auth.md)

> Secure sign-in and session persistence logic.

### 3D Studio & AR Flow

![Sequence Customization](./Interactions/sequence_customization.md)

> The customization pipeline from real-time 3D updates to AR projection.

### Recommendations & Tracking

![Sequence Recommendation](./Interactions/sequence_recommendation.md)

> Intelligent discovery and interaction tracking loop.
