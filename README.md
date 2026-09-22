# Connected Vehicle Telemetry System

A full-stack **Connected Vehicle Telemetry and Fleet Monitoring System** for tracking vehicle activity, speed, engine temperature, location, analytics, and fleet-level operations.

The project provides a React dashboard for clients and administrators, backed by a Spring Boot REST API, MySQL persistence, JWT authentication, role-based access control, historical telemetry seeding, and continuous simulated telemetry generation.

---

## 📌 Project Overview

The **Connected Vehicle Telemetry System** is designed to demonstrate how vehicle telemetry data can be collected, stored, processed, and visualized through a modern web application.

The system supports:

- Secure user authentication with JWT stored in an HttpOnly cookie
- Role-based access for **ADMIN** and **CLIENT** users
- Client-specific vehicle visibility
- Fleet overview and vehicle drill-down
- Speed and engine-temperature analytics
- Vehicle location visualization
- Multi-vehicle comparison
- Admin fleet and client management
- Historical telemetry data generation
- Continuous simulated live telemetry
- Responsive dashboard with light/dark theme support

> **Note:** This project uses a built-in telemetry simulator and seeded data. It does not require a physical vehicle, IoT device, or external telemetry hardware to run locally.

---

## ✨ Key Features

### 🔐 Authentication & Authorization

- User registration and login
- JWT-based authentication
- JWT stored using an HttpOnly cookie
- Stateless Spring Security configuration
- BCrypt password hashing
- Role-based authorization
- Protected frontend routes
- Admin-only routes and APIs
- Automatic session restoration using `/api/auth/me`
- Logout support

### 🚗 Vehicle Management

Clients can access the vehicles assigned to them.

Vehicle information includes:

- Vehicle ID
- Manufacturer
- Model
- Vehicle name
- Registration/vehicle code
- Registration date
- Owner

### 📡 Telemetry Monitoring

The application works with simulated vehicle telemetry containing:

- Vehicle speed
- Engine temperature
- Latitude
- Longitude
- Timestamp

The backend generates historical telemetry during initial setup and can continue producing simulated readings at a configurable interval.

### 📊 Analytics Dashboard

The dashboard provides:

- KPI summaries
- Speed analysis
- Temperature history
- Time-range filtering
- Multi-vehicle comparison
- Vehicle performance visualization
- Historical trend analysis

Charts are implemented using **Recharts**.

### 🗺️ Location Tracking

Vehicle coordinates can be visualized using **Leaflet** and **React Leaflet**.

The system can represent:

- Current/latest vehicle location
- Fleet locations
- Vehicle movement context

### 👨‍💼 Admin Dashboard

Administrators can access global fleet information and management functionality.

Admin functionality includes:

- System statistics
- Global fleet table
- Fleet map
- Top speed information
- Client management
- Client vehicle management
- Create clients
- Create vehicles for clients
- Delete clients
- Delete vehicles

### 🎨 UI Features

- React-based SPA
- Tailwind CSS styling
- Responsive dashboard layout
- Sidebar navigation
- Top navigation bar
- Dark/light theme
- Loading states
- Empty states
- Error boundary
- Vehicle selectors
- Date/time range controls
- KPI cards
- Interactive charts

---

# 🏗️ System Architecture

```text
                    ┌──────────────────────────┐
                    │      React Frontend      │
                    │        Vite SPA          │
                    │                          │
                    │ React Router              │
                    │ React Query               │
                    │ Axios                     │
                    │ Tailwind CSS              │
                    │ Recharts                  │
                    │ React Leaflet             │
                    └────────────┬─────────────┘
                                 │
                         HTTP / REST API
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │    Spring Boot Backend   │
                    │                          │
                    │ Controllers               │
                    │ Services                  │
                    │ Repositories              │
                    │ DTOs                      │
                    │ Spring Security           │
                    │ JWT Authentication        │
                    │ Telemetry Simulator       │
                    └────────────┬─────────────┘
                                 │
                              JPA/Hibernate
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │         MySQL             │
                    │                          │
                    │ users                     │
                    │ vehicles                  │
                    │ vehicle_readings          │
                    └──────────────────────────┘
```

---

# 🛠️ Technology Stack

## Frontend

| Technology | Purpose |
|---|---|
| React 18 | UI development |
| Vite | Frontend build tool |
| React Router | Client-side routing |
| Axios | REST API communication |
| TanStack React Query | Server-state/data fetching |
| Tailwind CSS | Styling |
| Recharts | Analytics charts |
| Leaflet | Maps |
| React Leaflet | React integration for Leaflet |
| Lucide React | Icons |

## Backend

| Technology | Purpose |
|---|---|
| Java | Backend programming language |
| Spring Boot 3.5 | REST API/application framework |
| Spring Web | REST controllers |
| Spring Data JPA | Database persistence |
| Hibernate | ORM |
| Spring Security | Authentication and authorization |
| JJWT | JWT generation/validation |
| MySQL Connector/J | MySQL connectivity |
| Lombok | Boilerplate reduction |
| Maven | Dependency/build management |

---

# 📂 Project Structure

```text
Connected-Vehicle-Telimetry-system/
│
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   │   ├── admin.js
│   │   │   ├── auth.js
│   │   │   ├── client.js
│   │   │   └── vehicles.js
│   │   │
│   │   ├── components/
│   │   │   ├── admin/
│   │   │   │   ├── FleetMap.jsx
│   │   │   │   ├── GlobalFleetTable.jsx
│   │   │   │   ├── SystemStatsCards.jsx
│   │   │   │   └── VehicleFilterBar.jsx
│   │   │   │
│   │   │   ├── auth/
│   │   │   │   ├── ProtectedRoute.jsx
│   │   │   │   └── RoleRoute.jsx
│   │   │   │
│   │   │   ├── common/
│   │   │   │   ├── Card.jsx
│   │   │   │   ├── CustomDateRange.jsx
│   │   │   │   ├── EmptyState.jsx
│   │   │   │   ├── ErrorBoundary.jsx
│   │   │   │   ├── HourlyRangeSlider.jsx
│   │   │   │   ├── KpiCard.jsx
│   │   │   │   ├── LastUpdated.jsx
│   │   │   │   ├── LoadingBlock.jsx
│   │   │   │   ├── SegmentedControl.jsx
│   │   │   │   ├── ThemeToggle.jsx
│   │   │   │   ├── TimeRangePicker.jsx
│   │   │   │   ├── VehicleMultiSelect.jsx
│   │   │   │   └── VehicleSelector.jsx
│   │   │   │
│   │   │   ├── compare/
│   │   │   │   └── ComparisonLineChart.jsx
│   │   │   │
│   │   │   ├── dashboard/
│   │   │   │   ├── KpiGrid.jsx
│   │   │   │   ├── SpeedAnalysisChart.jsx
│   │   │   │   └── VehicleInfoCard.jsx
│   │   │   │
│   │   │   ├── engine/
│   │   │   │   └── TemperatureHistoryChart.jsx
│   │   │   │
│   │   │   ├── fleet/
│   │   │   │   └── VehicleCard.jsx
│   │   │   │
│   │   │   ├── layout/
│   │   │   │   ├── AppLayout.jsx
│   │   │   │   ├── Sidebar.jsx
│   │   │   │   └── Topbar.jsx
│   │   │   │
│   │   │   └── map/
│   │   │       └── MapLite.jsx
│   │   │
│   │   ├── context/
│   │   │   ├── AuthContext.jsx
│   │   │   └── ThemeContext.jsx
│   │   │
│   │   ├── lib/
│   │   │   ├── constants.js
│   │   │   └── formatters.js
│   │   │
│   │   ├── pages/
│   │   │   ├── AdminClientManagementPage.jsx
│   │   │   ├── AdminDashboardPage.jsx
│   │   │   ├── AnalyticsPage.jsx
│   │   │   ├── EngineHealthPage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   ├── VehicleDetailPage.jsx
│   │   │   └── VehicleOverviewPage.jsx
│   │   │
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   │
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── postcss.config.js
│
├── backend/
│   ├── src/main/java/com/telemetry/
│   │   ├── controller/
│   │   │   ├── AdminController.java
│   │   │   ├── AuthController.java
│   │   │   └── VehicleController.java
│   │   │
│   │   ├── dto/
│   │   │   ├── auth/
│   │   │   └── admin/
│   │   │
│   │   ├── entity/
│   │   │   ├── Role.java
│   │   │   ├── User.java
│   │   │   ├── Vehicle.java
│   │   │   └── VehicleReading.java
│   │   │
│   │   ├── exception/
│   │   ├── repository/
│   │   ├── security/
│   │   │   ├── JwtAuthFilter.java
│   │   │   ├── JwtService.java
│   │   │   └── SecurityConfig.java
│   │   │
│   │   ├── seed/
│   │   │   └── DataSeeder.java
│   │   │
│   │   ├── service/
│   │   ├── simulator/
│   │   │   ├── SimState.java
│   │   │   └── VehicleSimulator.java
│   │   │
│   │   ├── util/
│   │   │   └── DistanceUtil.java
│   │   │
│   │   └── TelemetryApplication.java
│   │
│   ├── src/main/resources/
│   │   └── application.properties
│   │
│   └── pom.xml
│
└── README.md
```

---

# ⚙️ Prerequisites

Install the following before running the project.

### Required

- **JDK 25**
- **Maven 3.9+**
- **Node.js 18+**
- **npm**
- **MySQL 8.x**
- Git

Verify installations:

```bash
java -version
mvn -version
node -v
npm -v
mysql --version
```

> The backend `pom.xml` is configured for Java 25. Use a compatible JDK when building the backend.

---

# 🗄️ Database Setup

The application uses MySQL.

Create the database manually if preferred:

```sql
CREATE DATABASE vehicle_telemetry;
```

The configured JDBC URL also contains:

```text
createDatabaseIfNotExist=true
```

so MySQL can create the database automatically when the configured user has sufficient privileges.

### Default configuration

Open:

```text
backend/src/main/resources/application.properties
```

Current development configuration:

```properties
server.port=8082

spring.datasource.url=jdbc:mysql://localhost:3306/vehicle_telemetry?createDatabaseIfNotExist=true&serverTimezone=UTC&useSSL=false&allowPublicKeyRetrieval=true
spring.datasource.username=root
spring.datasource.password=root
```

Change the username/password to match your local MySQL installation.

---

# 🚀 Running the Backend

Open a terminal:

```bash
cd backend
```

Install/build dependencies:

```bash
mvn clean install
```

Run the application:

```bash
mvn spring-boot:run
```

The backend starts on:

```text
http://localhost:8082
```

---

# 💻 Running the Frontend

Open another terminal:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start the Vite development server:

```bash
npm run dev
```

The frontend runs at:

```text
http://localhost:5173
```

The Vite development server proxies `/api` requests to:

```text
http://localhost:8082
```

---

# 🔄 Application Startup Flow

When the backend starts:

```text
Spring Boot starts
       ↓
Connects to MySQL
       ↓
Hibernate validates/updates schema
       ↓
DataSeeder checks database
       ↓
Users are created if missing
       ↓
Vehicle + historical telemetry data are seeded
       ↓
Vehicle simulator starts
       ↓
REST API becomes available
       ↓
React frontend consumes API
```

---

# 🌱 Seeded Users

The application contains development seed users.

| Role | Email | Password |
|---|---|---|
| ADMIN | `admin@gmail.com` | `Admin@123` |
| CLIENT | `client1@gmail.com` | `Client@123` |
| CLIENT | `client2@gmail.com` | `Client@123` |
| CLIENT | `client3@gmail.com` | `Client@123` |

**These credentials are for local development only. Change/remove them before production deployment.**

---

# 🚗 Seeded Fleet

The initial dataset contains **10 vehicles** distributed across three client accounts.

The seeded fleet includes vehicles from manufacturers such as:

- Tata
- Mahindra
- Ashok Leyland
- Eicher
- Force
- BharatBenz
- Volvo

The exact telemetry dataset is generated by `DataSeeder`.

---

# 📡 Telemetry Generation

Historical telemetry is configurable through:

```properties
telemetry.seed.enabled=true
telemetry.seed.days=30
telemetry.seed.interval-minutes=1
```

The seed process generates vehicle readings containing:

```text
Speed
Engine Temperature
Latitude
Longitude
Timestamp
```

The application also has a continuous simulator:

```properties
telemetry.simulator.enabled=true
telemetry.simulator.tick-ms=60000
```

This allows the dashboard to work with continuously changing simulated telemetry without requiring physical vehicle hardware.

---

# 🔐 Authentication Flow

The application uses JWT authentication with an HttpOnly cookie.

```text
User
 │
 │ POST /api/auth/login
 ▼
AuthController
 │
 ▼
AuthService
 │
 ▼
Validate credentials
 │
 ▼
Generate JWT
 │
 ▼
Set HttpOnly auth_token cookie
 │
 ▼
Browser stores cookie
 │
 ▼
Subsequent /api requests
 │
 ▼
JwtAuthFilter
 │
 ▼
Validate JWT
 │
 ▼
Authenticated User
```

The cookie is configured with:

```text
HttpOnly
SameSite=Lax
Path=/
```

JWT expiry is configured in `application.properties`:

```properties
jwt.expiry-hours=24
```

---

# 🛡️ Role-Based Access

The application supports two roles:

```text
ADMIN
CLIENT
```

### CLIENT

Clients can:

- View their vehicles
- Open vehicle details
- View telemetry
- View KPIs
- Analyze speed
- Analyze engine temperature
- Compare vehicles they can access
- View location information

### ADMIN

Administrators can additionally:

- View global fleet
- View system statistics
- View fleet analytics
- Manage clients
- Create clients
- View client vehicles
- Create vehicles
- Delete clients
- Delete vehicles

---

# 🌐 Frontend Routes

| Route | Access | Purpose |
|---|---|---|
| `/login` | Public | Login |
| `/` | Authenticated | Vehicle/fleet overview |
| `/vehicles/:id` | Authenticated | Vehicle details |
| `/analytics` | Authenticated | Analytics dashboard |
| `/engine-health` | Authenticated | Engine temperature monitoring |
| `/admin/dashboard` | ADMIN | Global fleet dashboard |
| `/admin/clients` | ADMIN | Client and vehicle management |

The frontend uses:

```text
ProtectedRoute
RoleRoute
```

to enforce authentication and role-based navigation.

---

# 🔌 REST API

Base URL:

```text
http://localhost:8082/api
```

## Authentication

### Register

```http
POST /api/auth/register
```

### Login

```http
POST /api/auth/login
```

### Logout

```http
POST /api/auth/logout
```

### Current User

```http
GET /api/auth/me
```

---

## Vehicle APIs

### List Vehicles

```http
GET /api/vehicles
```

### Get Vehicle

```http
GET /api/vehicles/{id}
```

### Latest Reading

```http
GET /api/vehicles/{id}/latest
```

### Vehicle KPIs

```http
GET /api/vehicles/{id}/kpis?from={epochMs}&to={epochMs}
```

### Speed Chart

```http
GET /api/vehicles/{id}/speed-chart?period=week
```

Supported periods:

```text
day
week
month
```

### Temperature History

```http
GET /api/vehicles/{id}/temperature-history?from={epochMs}&to={epochMs}
```

### Vehicle Comparison

```http
GET /api/vehicles/compare?ids=1,2,3&metric=speed&from={epochMs}&to={epochMs}
```

Supported metrics include:

```text
speed
temp
```

---

# 👨‍💼 Admin APIs

### System Statistics

```http
GET /api/admin/stats
```

### Global Fleet

```http
GET /api/admin/fleet
```

### Top Speed Today

```http
GET /api/admin/top-speed-today
```

### List Clients

```http
GET /api/admin/clients
```

### Create Client

```http
POST /api/admin/clients
```

### List Client Vehicles

```http
GET /api/admin/clients/{clientId}/vehicles
```

### Create Client Vehicle

```http
POST /api/admin/clients/{clientId}/vehicles
```

### Delete Client

```http
DELETE /api/admin/clients/{clientId}
```

### Delete Vehicle

```http
DELETE /api/admin/clients/{clientId}/vehicles/{vehicleId}
```

Admin endpoints require an authenticated user with the `ADMIN` role.

---

# 🗃️ Database Model

The primary entities are:

```text
User
 │
 └── owns ──> Vehicle
                  │
                  └── has ──> VehicleReading
```

### User

Contains:

- ID
- Email
- Password hash
- Full name
- Role
- Creation timestamp

### Vehicle

Contains:

- Vehicle ID
- Manufacturer
- Model
- Vehicle name
- Vehicle code
- Registration date
- Owner

### VehicleReading

Contains:

- Reading ID
- Vehicle ID
- Speed
- Engine temperature
- Latitude
- Longitude
- Timestamp

---

# 📈 Telemetry Analytics

The backend processes raw telemetry into dashboard-friendly DTOs.

Examples include:

```text
KpiDto
SpeedChartDto
TempPointDto
CompareDto
CompareSeriesDto
SpeedBucketDto
ReadingDto
```

This keeps the frontend focused on presentation rather than implementing business calculations.

---

# 🧮 Location Distance Calculation

The backend contains:

```text
DistanceUtil.java
```

which provides geographic distance calculations based on latitude and longitude.

This supports telemetry/fleet location analysis.

---

# 🎨 Theme Support

The application supports light and dark themes.

Theme state is handled through:

```text
frontend/src/context/ThemeContext.jsx
```

The selected theme is persisted in browser `localStorage` using:

```text
vt-theme
```

---

# 🧪 Development Commands

## Frontend

Install packages:

```bash
npm install
```

Run development server:

```bash
npm run dev
```

Build production bundle:

```bash
npm run build
```

Preview production build:

```bash
npm run preview
```

## Backend

Build:

```bash
mvn clean install
```

Run:

```bash
mvn spring-boot:run
```

Package:

```bash
mvn clean package
```

---

# ⚙️ Important Configuration

The main backend configuration is:

```text
backend/src/main/resources/application.properties
```

Important properties:

```properties
server.port=8082

spring.datasource.url=...
spring.datasource.username=root
spring.datasource.password=root

jwt.secret=...
jwt.expiry-hours=24
jwt.cookie-name=auth_token

app.cors.allowed-origin=http://localhost:5173

telemetry.seed.enabled=true
telemetry.seed.days=30
telemetry.seed.interval-minutes=1

telemetry.simulator.enabled=true
telemetry.simulator.tick-ms=60000
```

---

# 🔒 Production Security Recommendations

The repository currently contains development configuration. Before deploying to production:

### 1. Change the database password

Do not use:

```properties
spring.datasource.password=root
```

### 2. Change the JWT secret

Do not use the development secret:

```properties
jwt.secret=dev-secret-change-me...
```

Use a strong randomly generated secret stored in an environment variable or secret manager.

### 3. Do not commit credentials

Use environment-specific configuration.

### 4. Use HTTPS

Configure HTTPS/TLS for both frontend and backend.

### 5. Secure cookies

For production, review:

```text
Secure
HttpOnly
SameSite
```

cookie settings according to the deployment architecture.

### 6. Disable development seed data

For production:

```properties
telemetry.seed.enabled=false
```

### 7. Review CORS

Replace:

```properties
app.cors.allowed-origin=http://localhost:5173
```

with the actual production frontend domain.

---

# 🐛 Troubleshooting

## MySQL connection refused

Check whether MySQL is running:

```bash
mysql -u root -p
```

On macOS with Homebrew:

```bash
brew services list
```

Start MySQL if necessary:

```bash
brew services start mysql
```

---

## Access denied for MySQL user

Check:

```properties
spring.datasource.username
spring.datasource.password
```

and verify that the credentials work independently:

```bash
mysql -u root -p
```

---

## Frontend cannot connect to backend

Confirm:

```text
Backend → http://localhost:8082
Frontend → http://localhost:5173
```

Also verify the Vite proxy:

```javascript
proxy: {
  '/api': {
    target: 'http://localhost:8082',
    changeOrigin: true
  }
}
```

---

## CORS error

Verify:

```properties
app.cors.allowed-origin=http://localhost:5173
```

and make sure the frontend is actually running on port `5173`.

---

## No vehicle data appears

Check:

```properties
telemetry.seed.enabled=true
```

If the `vehicle` table already contains data, the vehicle/reading seed is skipped.

For a clean development reseed, stop the application and clear the relevant database data before restarting.

---

## JWT authentication issues

Check:

- Backend is running
- Browser allows cookies
- Frontend API requests use credentials
- JWT cookie is present
- JWT secret is unchanged during the active session
- Frontend and backend origins match the CORS configuration

---

# 📊 Example User Flow

### Client

```text
Login
  ↓
Vehicle Overview
  ↓
Select Vehicle
  ↓
Vehicle Details
  ↓
View Latest Telemetry
  ↓
View Speed Analytics
  ↓
View Engine Health
  ↓
View Location
  ↓
Compare Vehicles
```

### Admin

```text
Login
  ↓
Admin Dashboard
  ↓
Global Fleet
  ↓
Fleet Statistics
  ↓
Client Management
  ↓
Create Client
  ↓
Add Vehicle
  ↓
Monitor Fleet
```

---

# 🚀 Future Enhancements

The architecture can be extended with:

- Real IoT/vehicle gateway integration
- MQTT telemetry ingestion
- WebSocket/SSE live updates
- Real-time alerts
- Geofencing
- Route history
- Fuel consumption monitoring
- Battery/EV monitoring
- Predictive maintenance
- ML-based anomaly detection
- Driver behavior analytics
- Notification system
- Email/SMS alerts
- Advanced fleet reports
- CSV/PDF export
- Cloud deployment
- Docker/Kubernetes deployment
- Redis caching
- Kafka-based telemetry ingestion
- Prometheus/Grafana monitoring

---

# 📌 Project Highlights

This project demonstrates practical implementation of:

- Full-stack development
- React application architecture
- REST API design
- Spring Boot
- Spring Security
- JWT authentication
- Role-based authorization
- MySQL
- JPA/Hibernate
- Data seeding
- Telemetry simulation
- Data aggregation
- Analytics dashboards
- Interactive charts
- Geographic visualization
- API integration
- Responsive UI
- Error handling
- Production-oriented configuration

---

# 👨‍💻 Project Information

**Project:** Connected Vehicle Telemetry System

**Architecture:** Full Stack Web Application

**Frontend:** React + Vite

**Backend:** Spring Boot + Java

**Database:** MySQL

**Authentication:** JWT + HttpOnly Cookie

**Visualization:** Recharts + Leaflet

**Build Tools:** npm + Maven

---

# 📄 License

This project is intended for educational, portfolio, and demonstration purposes unless a separate license is provided.

---

## ⭐ If You Find This Project Useful

Consider improving the project by integrating a real telemetry source, adding real-time WebSocket updates, implementing predictive maintenance, and deploying the system using a cloud platform.
