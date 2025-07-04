# TaskMaster - Notion-like Task Manager

This project is a simple task management application inspired by Notion, featuring a frontend built with HTML, CSS (TailwindCSS), and JavaScript, and a backend powered by Java Spring Boot with MongoDB.

## Features

*   **Frontend:**
    *   Clean and responsive UI using TailwindCSS.
    *   Add new tasks with title, description, due date, category (tags), and priority.
    *   Display existing tasks.
    *   Mark tasks as complete/pending.
    *   Delete tasks.
    *   Connects to a RESTful API backend.

*   **Backend (Java Spring Boot):**
    *   RESTful API for CRUD (Create, Read, Update, Delete) operations on tasks.
    *   Uses Spring Data MongoDB for seamless database interaction.
    *   Automatic timestamping for `createdAt` and `updatedAt` fields.
    *   Configured with CORS to allow frontend communication.

## Technologies Used

*   **Frontend:** HTML, CSS (TailwindCSS), JavaScript (Fetch API)
*   **Backend:** Java 17+, Spring Boot 3.2.x, Spring Data MongoDB, Lombok
*   **Database:** MongoDB
*   **Build Tool:** Maven

## Prerequisites

Before you begin, ensure you have the following installed:

*   **Java Development Kit (JDK):** Version 17 or higher.
*   **Apache Maven:** Version 3.6.x or higher.
*   **MongoDB:** A running MongoDB instance (local or cloud-based).
    *   If running locally, ensure it's accessible on `mongodb://localhost:27017`.
*   **Web Browser:** Chrome, Firefox, Edge, etc.

## Setup and Running the Application

Follow these steps to get the TaskMaster application up and running.

### 1. Backend Setup (Java Spring Boot)

1.  **Clone the Repository (or create files manually):**
    If you're starting from scratch, create a new Maven project and add the files as described above in the `Project Structure`.

2.  **Navigate to the Backend Directory:**
    Open your terminal or command prompt and navigate to the `taskmaster-backend` directory (the one containing `pom.xml`).

    ```bash
    cd path/to/your/taskmaster-backend
    ```

3.  **Configure MongoDB Connection:**
    Open `src/main/resources/application.properties` and ensure the `spring.data.mongodb.uri` points to your running MongoDB instance. The default `mongodb://localhost:27017/taskmasterdb` should work for a local MongoDB setup.

4.  **Build the Backend Application:**
    Use Maven to build the project. This will download dependencies and compile the code.

    ```bash
    mvn clean install
    ```

5.  **Run the Backend Application:**
    After a successful build, you can run the Spring Boot application.

    ```bash
    mvn spring-boot:run
    ```
    The backend will start on `http://localhost:8080`. You should see logs indicating that Spring Boot has started and connected to MongoDB.

### 2. Frontend Setup (HTML/CSS/JavaScript)

The frontend is a single `frontend.html` file.

1.  **Locate `frontend.html`:**
    Ensure you have the `frontend.html` file (provided above) saved in a convenient location.

2.  **Open in Browser:**
    Simply open the `frontend.html` file directly in your web browser.
    *   **Important:** If you open it directly (e.g., `file:///C:/path/to/frontend.html`), browsers treat its origin as "null". The backend's CORS configuration (`WebConfig.java`) includes `"null"` in `allowedOrigins` to accommodate this.
    *   **Recommended for Development:** For a better development experience, you can use a simple local web server (e.g., `npx live-server` if you have Node.js installed). If you use `live-server`, it typically serves on `http://127.0.0.1:8080` or `http://localhost:8080`. The CORS configuration already includes these.

    ```bash
    # If you have Node.js and npm installed
    npm install -g live-server
    live-server path/to/directory/containing/frontend.html
    ```

## Testing the Application

1.  **Ensure Backend is Running:** Verify that your Spring Boot application is running in the terminal (look for "Started TaskmasterApplication in X.XXX seconds").
2.  **Ensure MongoDB is Running:** Confirm your MongoDB server is active.
3.  **Open Frontend:** Open `frontend.html` in your browser.
4.  **Add Tasks:** Click the "+ New Task" button, fill in the details, and click "Save Task". You should see the new task appear in the list.
5.  **Check CRUD Operations:**
    *   **Create:** Add a new task.
    *   **Read:** Tasks should load automatically when the page loads, and new tasks appear after creation.
    *   **Update (Status):** Click the checkbox next to a task to mark it as completed/pending.
    *   **Delete:** Click the trashcan icon next to a task to delete it. Confirm the deletion.

## Troubleshooting

*   **"Failed to load tasks" / CORS Errors in Browser Console:**
    *   Ensure your Spring Boot backend is running.
    *   Check the `server.port` in `application.properties` matches the port in `frontend.html` (`backendBaseUrl`).
    *   Verify the `WebConfig.java` CORS configuration in the backend. Make sure `allowedOrigins` includes the exact origin from which your `frontend.html` is being served (e.g., `http://localhost:8080`, `http://127.0.0.1:8080`, or `null` for `file://` access).
*   **"Failed to connect to MongoDB" in Backend Logs:**
    *   Ensure your MongoDB server is running.
    *   Check the `spring.data.mongodb.uri` in `application.properties` for correctness (hostname, port, database name).
*   **Tasks not appearing/not saving:**
    *   Check your browser's developer console for any JavaScript errors.
    *   Check the backend terminal for any Java exceptions or error messages.
    *   Verify the JSON structure sent from the frontend matches the `Task` model in Java.
*   **`id` vs `_id`:** Spring Data MongoDB automatically maps the `id` field in your `Task.java` model to MongoDB's `_id` field. The frontend should use `task.id` when referring to the unique identifier.

---

This comprehensive setup should get your Java Spring Boot backend with MongoDB and the HTML frontend working together correctly, performing all CRUD operations. Remember to follow the `README.md` instructions carefully.