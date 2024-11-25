# Maathru - Maternal and Infant Health Support System

<p align="center" width="100%">
    <img width="33%" src="./logo.png" alt="Maathru Logo">
</p>


#### Group 27
#### SCS3214/IS3113 Group Project II

This document provides detailed instructions for setting up and running the **Maathru - Maternal and Infant Health Support System** locally. Follow the steps below for a successful deployment.

---

## Prerequisites

### Install Docker Desktop (Recommended)

#### Windows
1. Download **Docker Desktop for Windows** from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
2. Install Docker Desktop:
   - Run the installer and follow the on-screen instructions.
   - Ensure that **WSL 2** is enabled during installation.
3. Start Docker Desktop and confirm that it is running:
   ```bash
   docker --version
   docker-compose --version
   ```

#### macOS
1. Download **Docker Desktop for Mac** from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
2. Install Docker Desktop:
   - Open the `.dmg` file and drag Docker to your Applications folder.
   - Open Docker from Applications and follow the setup instructions.
3. Verify installation:
   ```bash
   docker --version
   docker-compose --version
   ```

#### Ubuntu (Linux)
1. Download the **Docker Desktop for Linux** installer:
   - Visit [Docker Desktop](https://www.docker.com/products/docker-desktop) and download the `.deb` package for Ubuntu (or any other Debian based system).
2. Install Docker Desktop:
   - Open a terminal at the path of the downloaded file and run:
     ```bash
     sudo apt install ./docker-desktop-<version>-<arch>.deb
     ```
     Replace `<version>` and `<arch>` with the downloaded file's version and architecture.
3. Start Docker Desktop:
   - Launch Docker Desktop and confirm that it is running:
     ```bash
     docker --version
     docker-compose --version
     ```

---

## Deployment Methods

### Docker-Compose Deployment

#### Step 1: Clone the Repositories
Clone the project repositories:
```bash
git clone https://github.com/Maathru/Frontend-Web-.git
git clone https://github.com/Maathru/Backend.git
```

#### Step 2: Configure Environment Variables

**Frontend:**
1. Navigate to the `Frontend-Web-` directory:
   ```bash
   cd Frontend-Web-
   ```
2. Create a `.env` file:
   ```bash
   touch .env
   ```
3. Add the following environment variables:
   ```env
   BACKEND_API_URL=http://localhost:8080/api/v1
   GOOGLE_MAPS_API_KEY=<your-api-key>
   ```

**Backend:**
No separate `.env` file is needed, as environment variables are included directly in the `docker-compose.yml` file for the backend for ease of test deployment.

#### Step 3: Start the Application
Navigate to the respective directories and start the containers.

**Frontend:**
```bash
cd Frontend-Web-
docker-compose up -d
```

**Backend:**
```bash
cd Backend
docker-compose up -d
```

#### Step 4: Access the Application on 
`http://localhost:5173`

---

### Manual Deployment

#### Frontend

1. **Install Node.js**:
   Ensure Node.js and Yarn are installed:
   ```bash
   node --version
   yarn --version
   ```

2. **Setup and Run**:
   - Navigate to the frontend directory:
     ```bash
     cd Frontend-Web-
     ```
   - Install dependencies:
     ```bash
     yarn install
     ```
   - Create a `.env` file:
     ```bash
     touch .env
     ```
   - Add the following environment variables:
     ```env
     BACKEND_API_URL=http://localhost:8080/api/v1
     GOOGLE_MAPS_API_KEY=<your-api-key>
     ```
   - Start the development server:
     ```bash
     yarn dev
     ```
   - Access the frontend at `http://localhost:5173`.

#### Backend

1. **Install Java**:
   Ensure JDK 17 is installed:
   ```bash
   java --version
   ```

2. **Setup Database**:
   - Install PostgreSQL and create a database:
     ```bash
     sudo -u postgres psql
     CREATE DATABASE maathru;
     CREATE USER postgres WITH PASSWORD 'password';
     GRANT ALL PRIVILEGES ON DATABASE maathru TO postgres;
     ```

3. **Build and Run**:
   - Navigate to the backend directory:
     ```bash
     cd Backend
     ```
   - Build the project:
     ```bash
     ./mvnw package
     ```
   - Run the application:
     ```bash
     java -jar target/backend-0.0.1-SNAPSHOT.jar
     ```
   - Access the API at `http://localhost:8080/api/v1`.

---

## Troubleshooting

### Common Docker Issues
1. **Containers Not Starting**:
   Check logs:
   ```bash
   docker-compose logs -f
   ```
2. **Database Connection Issues**:
   Ensure PostgreSQL is running and accessible.

### Manual Deployment Issues
1. **Frontend Not Starting**:
   Verify dependencies are installed and no ports are blocked.
2. **Backend Fails**:
   Confirm the database credentials match the configuration.

---

## Stopping the Application

To stop Docker containers:
```bash
docker-compose down
```

To stop manually run applications, use `Ctrl+C` in their respective terminals.

---

## Notes
- Replace default credentials and secrets for production deployment.
- Consider adding HTTPS for secure communication.
