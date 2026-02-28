# 📊 AR Car Showcase - UML Documentation

This document serves as the detailed manifest for all the Unified Modeling Language (UML) diagrams generated for the AR Car Showcase.

**Looking for a single-page overview with visual previews?** 
Check out the [Categorized UML Reference](../src/main/resources/Project_UML_Docs/Categorized_UML_Reference.md).

---

### 🏗️ 1. Structural Architecture
These diagrams focus on the static architecture and service relationships of the AR Car Showcase ecosystem.
*   **[System Architecture](../src/main/resources/Project_UML_Docs/Structural/architecture_diagram.md):** A high-level overview showing the React Native frontend communicating with the Spring Boot backend and Python Blender engines.
*   **[Component Structure](../src/main/resources/Project_UML_Docs/Structural/component_diagram.md):** A modular breakdown showing state management, navigation layers, and service boundaries.
*   **[Class Diagram (Core Logic)](../src/main/resources/Project_UML_Docs/Structural/class_diagram_core.md):** Defines relationships between context providers, authentication logic, and the `Car` data entities.

---

### 🚦 2. Behavioral Flows
These flowcharts map the dynamic functionality and user journey through the application.
*   **[Application Use Cases](../src/main/resources/Project_UML_Docs/Behavioral/use_case_diagram.md):** An overview of all primary user actions, from browsing catalogs to 3D AR projection.
*   **[App State Machine](../src/main/resources/Project_UML_Docs/Behavioral/state_diagram.md):** Illustrates the app navigation states between Guest viewers and Authenticated users entering the AR studio.
*   **[User Journey (Activity Flow)](../src/main/resources/Project_UML_Docs/Behavioral/activity_diagram.md):** A step-by-step logic map tracing a user's journey from app launch down to projecting a life-sized car in reality.

---

### 🔄 3. Interaction & Sequence Flows
These diagrams illustrate the chronological exchange of JSON payloads and HTTP requests between the mobile UI and backend nodes.
*   **[Authentication Flow](../src/main/resources/Project_UML_Docs/Interactions/sequence_auth.md):** Shows the secure sign-in process, token retrieval, and local persistence.
*   **[3D Customization & AR Projection Flow](../src/main/resources/Project_UML_Docs/Interactions/sequence_customization.md):** Details exactly how a hex color picked by the user goes to the backend, spins up the Blender `.glb` generation, and streams down to the ViroReact AR engine.
*   **[Recommendation & Auto-Search Flow](../src/main/resources/Project_UML_Docs/Interactions/sequence_recommendation.md):** Explains how user behavior feeds into the machine learning models and returns personalized car configurations in real-time.
