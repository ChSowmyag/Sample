# 🚀 Getting Started & Setup Instructions

The AR Car Showcase backend consists of two main applications running concurrently:
1.  **Spring Boot Core Server** (Java 17 / PostgreSQL)
2.  **Blender Microservice** (Python 3.10+)

Follow the steps below to initialize the repository locally.

---

### Prerequisites
*   **Java 17** & **Maven**
*   **PostgreSQL 15**
*   **Python 3.10+**
*   **Blender 3.x or 4.x** (Installed locally and added to your system PATH)

---

### Phase 1: Database Setup
1. Create a PostgreSQL database named `ar_car_showcase` (or update `application.properties` to match your existing DB).
2. Configure your DB credentials in the Spring Boot configuration file located at `src/main/resources/application.properties`.

---

### Phase 2: Running the Spring Boot Server
1. Navigate to the root directory of the backend repository.
2. Build and run the Maven project:
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```
3. The core API server will start on port `8080`.

---

### Phase 3: Running the Blender Python Service
This service intercepts requests from the Spring boot application to dynamically assemble 3D `.glb` files.

1. Navigate to the python microservice directory (adjust path based on your exact repository structure, e.g., `cd blender-service` or `cd src/main/python`).
2. Set up a Python virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `.\venv\Scripts\activate`
   ```
3. Install the required Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Start the application:
   ```bash
   python app.py  # Or run via flask/fastapi depending on your framework
   ```
5. Ensure that the `bpy` (Blender Python module) successfully initializes. The microservice typically runs on port `5000` or `8000` and receives REST calls directly from the Spring Boot API whenever a user clicks "View in AR" on the mobile client.
