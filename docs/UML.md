# 📊 AR Car Showcase - UML Documentation

This document serves as the detailed manifest for all the Unified Modeling Language (UML) diagrams generated for the AR Car Showcase.

---

### 🏗️ 1. Structural Architecture
These diagrams focus on the static architecture and service relationships of the AR Car Showcase ecosystem.

#### System Architecture
A high-level overview showing the React Native frontend communicating with the Spring Boot backend and Python Blender engines.
```mermaid
graph TB
    subgraph "Mobile Client (React Native / Expo SDK 50+)"
        UI["User Interface (React Native Screens)"]
        Context["State Management (React Context API)"]
        API_Client["Network Layer (Fetch/AsyncStorage)"]

        subgraph "Interactive Engines"
            AR_Scene["AR Hybrid Scene (ViroReact)"]
            Studio_3D["3D Model Viewer (React Three Fiber)"]
            Gesture_Handler["Gesture Logic (Reanimated)"]
        end
    end

    subgraph "Distributed Backend (Cloud Hosted)"
        Main_Server["Spring Boot API (Java 17/Maven)"]
        Blender_Service["Blender Microservice (Python/FastAPI)"]
        Rec_Engine["Recommendation Engine (Java/PostgreSQL)"]
        DB[(PostgreSQL 15 / Persistence)]
    end

    %% Relationships
    UI --> Context
    Context --> API_Client
    API_Client <--> Main_Server

    UI --> AR_Scene
    UI --> Studio_3D
    Studio_3D --> Gesture_Handler
    AR_Scene --> Gesture_Handler

    Main_Server <--> DB
    Main_Server <--> Blender_Service
    Main_Server <--> Rec_Engine

    Blender_Service -.-> |"Binary GLB Stream"| AR_Scene
    Rec_Engine -.-> |"JSON Preferences"| UI
```

#### Component Structure
A modular breakdown showing state management, navigation layers, and service boundaries.
```mermaid
graph TB
    App[App Flow / Router]

    subgraph Navigation_Layer ["Navigation Layer"]
        Drawer[Drawer Layout]
        Tabs[Tabs Layout]
    end

    subgraph State_Management ["State Management"]
        AuthCtx[AuthContext]
        CarCtx[CarContext]
        ThemeCtx[ThemeContext]
    end

    subgraph Feature_Components ["Feature Components"]
        Studio[3D Studio / Hybrid]
        AR[AR Scenes]
        Catalog[Car Catalog]
        Compare[Comparison View]
        Prefs[Personalization]
    end

    subgraph Service_Layer ["Service Layer"]
        Client[API Client]
        Blender[Blender Service]
        Rec[Recommendation Service]
    end

    App --> Drawer
    Drawer --> Tabs

    Tabs --> Catalog
    Tabs --> Prefs

    Catalog --> Studio
    Studio --> AR

    Studio --> CarCtx
    AR --> CarCtx

    AuthCtx --> Client
    CarCtx --> Client

    Client --> Blender
    Client --> Rec
```

#### Class Diagram (Core Logic)
Defines relationships between context providers, authentication logic, and the `Car` data entities.
```mermaid
classDiagram
    class AuthContext {
        +User user
        +boolean isLoading
        +boolean isAuthenticated
        +signIn(username, password)
        +signUp(username, email, password)
        +signOut()
    }

    class CarContext {
        +CarConfig config
        +updateMaterialColor(name, hex)
        +updateVehicle(car)
        +resetCustomization()
    }

    class apiClient {
        +BASE_URL
        +get(endpoint, params)
        +post(endpoint, data)
        +setUnauthorizedHandler(fn)
    }

    class carsApi {
        +getAllCars()
        +getCarById(id)
        +searchCars(query)
    }

    class blenderService {
        +generateCustomModel(vehicleId, materials)
        +getModelUrl(filename)
    }

    class Car {
        +int id
        +string brand
        +string model
        +string fuelType
        +string transmissionType
        +CarImages images
        +string model3D
        +Record specs
    }

    class Customization {
        +int id
        +int carId
        +Map~String,String~ materials
        +String generatedUrl
    }

    class Recommendation {
        +int userId
        +List~Car~ suggestedCars
        +trackInteraction(carId, type)
    }

    AuthContext ..> apiClient : uses
    CarContext ..> apiClient : uses
    carsApi ..> Car : fetches
    blenderService ..> apiClient : uses
    CarContext --> Car : manages selected
    CarContext --> Customization : tracks current
    Recommendation ..> Car : suggests
```

---

### 🚦 2. Behavioral Flows
These flowcharts map the dynamic functionality and user journey through the application.

#### Application Use Cases
An overview of all primary user actions, from browsing catalogs to 3D AR projection.
```mermaid
graph TD
    User((User))
    Sys[Backend System / Microservices]

    subgraph "AR Car Showcase Application"
        UC1(Browse Car Catalog)
        UC2(View Detailed Specs)
        UC3(3D Customization Workspace)
        UC4(Hyper-Realistic AR Projection)
        UC5(Side-by-Side Comparison)
        UC6(AI-Driven Recommendations)
        UC7(Personal Showroom)
        UC8(Secure User Auth)
    end

    User --> UC1
    User --> UC2
    User --> UC3
    User --> UC5
    User --> UC7
    User --> UC8

    UC3 -.-> |includes| UC4
    UC2 -.-> |extends| UC6
    UC7 -.-> |requires| UC8
    UC3 -.-> |requires| UC8

    UC1 --- Sys
    UC3 --- Sys
    UC6 --- Sys
    UC7 --- Sys
    UC8 --- Sys
```

#### App State Machine
Illustrates the app navigation states between Guest viewers and Authenticated users entering the AR studio.
```mermaid
stateDiagram-v2
    [*] --> Guest_State

    state Guest_State {
        [*] --> Home_Browse
        Home_Browse --> Details_View
        Details_View --> Home_Browse
        Details_View --> 3D_Studio_Limited
    }

    Guest_State --> Authenticated_State : Login Success

    state Authenticated_State {
        [*] --> Dashboard
        Dashboard --> Customization_Studio
        Customization_Studio --> AR_Mode
        AR_Mode --> Customization_Studio

        Dashboard --> Comparison_Tool
        Dashboard --> Personal_Showroom

        state Customization_Studio {
            [*] --> Exterior_View
            Exterior_View --> Interior_View
            Interior_View --> Exterior_View
        }
    }

    Authenticated_State --> Guest_State : Logout
```

#### User Journey (Activity Flow)
A step-by-step logic map tracing a user's journey from app launch down to projecting a life-sized car in reality.
```mermaid
flowchart TD
    Start((Start)) --> Launch[User Launches App]
    Launch --> CheckLogin{Is Logged In?}
    
    CheckLogin -- No --> Browse[Browse Generic Catalog]
    Browse --> ViewDetailsGuest[View Car Details]
    ViewDetailsGuest --> WantsCustom{User wants to customize?}
    WantsCustom -- Yes --> Prompt[Prompt Login]
    Prompt --> EndGuest(((End)))
    WantsCustom -- No --> EndGuest
    
    CheckLogin -- Yes --> Recs[View Personalized Recommendations]
    Recs --> Search[Search/Select Specific Car]
    Search --> Studio[Open 3D Studio]
    
    Studio --> PickMat[Pick Material: Paint, Wheels, etc.]
    PickMat --> ApplyCol[Apply Color/Texture]
    ApplyCol --> Manipulate[Manipulate Model: Rotate/Zoom]
    Manipulate --> Satisfied{User Satisfied?}
    
    Satisfied -- No --> PickMat
    Satisfied -- Yes --> ActionsFork((Fork))
    
    ActionsFork --> Save[Save to My Showroom]
    ActionsFork --> LaunchAR[Launch AR Experience]
    
    LaunchAR --> Surface[Find Horizontal Surface]
    Surface --> Place[Place Car in Real World]
    Place --> Snap[Take Screenshot/View]
    
    Save --> Join((Join))
    Snap --> Join
    Join --> EndAuth(((End)))
```

---

### 🔄 3. Interaction & Sequence Flows
These diagrams illustrate the chronological exchange of JSON payloads and HTTP requests between the mobile UI and backend nodes.

#### Authentication Flow
Shows the secure sign-in process, token retrieval, and local persistence.
```mermaid
sequenceDiagram
    participant U as User
    participant UI as LoginScreen
    participant AC as AuthContext
    participant CL as API Client
    participant S as Backend Server
    participant AS as AsyncStorage

    U->>UI: Enter Credentials
    UI->>AC: signIn(user, pass)
    AC->>CL: post('/auth/signin')
    CL->>S: Request JSON
    S-->>CL: Response (JWT + User Data)
    CL-->>AC: Adapted Data

    alt Success
        AC->>AS: Save Token & User Body
        AC->>UI: Update Auth State
        UI->>U: Navigate to Home
    else Failure
        AC->>UI: Return Error Message
        UI->>U: Display Alert
    end
```

#### 3D Customization & AR Projection Flow
Details exactly how a hex color picked by the user goes to the backend, spins up the Blender `.glb` generation, and streams down to the ViroReact AR engine.
```mermaid
sequenceDiagram
    participant U as User
    participant HS as HybridScreen (3D Studio)
    participant CC as CarContext (React)
    participant CD as CustomizationDrawer
    participant AR as ARHybridScene (Viro)
    participant BV as Blender Microservice (Python)

    U->>HS: Select Car from Catalog
    HS->>CC: updateVehicle(carData)
    U->>HS: Toggle Customizer Workspace
    HS->>CD: mount(isPickerVisible=true)

    U->>CD: Modify Material Color (e.g. #FF0000)
    CD->>CC: updateMaterialColor(part, color)
    CC-->>HS: trigger(r3f-re-render)
    HS->>HS: Apply Material to Mesh Object

    U->>HS: Click "Apply to AR"

    HS->>BV: generateCustomModel(vehicleId, materials)
    activate BV
    BV->>BV: Load Base .blend
    BV->>BV: Update Cycles/Eevee Materials
    BV->>BV: Export .glb Stream
    BV-->>HS: Return Model Metadata & Filename
    deactivate BV

    HS->>HS: setGeneratedModelUrl(newUrl)
    HS->>HS: setViewMode('AR')

    HS->>AR: mount(viroAppProps)
    AR->>AR: initialize(ARSession)
    AR->>HS: onModelLoadStart()
    HS->>U: Display "Generating Model..." (Spinner)
    AR->>AR: fetch(customModelUrl)
    AR-->>U: Project Customized Car in AR
```

#### Recommendation & Auto-Search Flow
Explains how user behavior feeds into the machine learning models and returns personalized car configurations in real-time.
```mermaid
sequenceDiagram
    participant U as User
    participant SC as Search/Home Screen
    participant AC as AuthContext
    participant RA as Recommendation API
    participant S as Spring Boot Server
    participant RE as JAVA Recommendation Engine

    U->>SC: Enter Search Query / View Home
    SC->>AC: Get User Preferences
    SC->>RA: getUserRecommendations()
    RA->>S: GET /personalized
    S->>RE: Query Preferred Matches
    RE-->>S: List of Recommended Cars
    S-->>RA: JSON Data
    RA-->>SC: Map to UI Components
    SC->>U: Display "Recommended for You"

    U->>SC: Click on a Car
    SC->>RA: trackInteraction(carId, 'view')
    RA->>S: POST /feedback
    S->>RE: Update User Behavior Model
```
