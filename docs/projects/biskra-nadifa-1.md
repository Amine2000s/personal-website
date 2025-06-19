# ♻️ Biskra Nadifa – Smart Waste Management System for Biskra



## 🔍 Overview



**Biskra Nadifa** (Arabic: "A Clean Biskra") is a **waste management platform** designed to address the escalating **problem of unmanaged trash in Biskra city** , Algeria. It facilitates digital coordination between citizens, cleaning agents (drivers), and system administrators to ensure responsive and efficient urban sanitation.

![biskra-nadifa-overview](../assets/images/blog/biskra-nadifa-1/biskra-nadifa-overview.png){loading=lazy}


This project was originally built as a **demonstrative MVP for a university graduation project**, with a **complete backend system developed using Spring Boot**.


---



github repo : ```https://github.com/Amine2000s/Biskra-nadifa-Backend-App```


## 🛠️ Tech Stack

- Java 17
- Spring Boot
- Spring Data JPA (Hibernate)
- MySQL
- Swagger (OpenAPI)
- Maven

---

## 🧠 Architecture

### 👥 Users

| Role           | Responsibilities                                                                          |
|----------------|-------------------------------------------------------------------------------------------|
| **Citizen**    | Submits trash reports (type, location, image), provides suggestions via mobile app        |
| **Driver**     | Views assigned cleanup tasks, updates task status via mobile app                          |
| **System User**| Validates reports, assigns tasks to the most appropriate driver via dashboard             |

### 🗂 Modules

- **Citizen Module**
- **Truck Driver Module**
- **System Admin Module**

---

### 🗺️ General Architecture

![General Architecture](../assets/images/blog/biskra-nadifa-1/general_architecture.png)

### 📊 ER Diagram

![ER Diagram](../assets/images/blog/biskra-nadifa-1/ER_diagram.png)

---

## 🎯 Key Features

| Feature                            | Description                                                                 |
|------------------------------------|-----------------------------------------------------------------------------|
| 📸 Report Submission               | Citizens submit trash location, type, and image evidence                    |
| 👤 Role-based Modules             | Modular separation of logic for each user category                          |
| 📍 Task Assignment Workflow       | System users assign tasks manually based on citizen reports                 |
| 🚚 Driver Dashboard               | Drivers view, update, and manage assigned cleanup tasks                     |
| 📝 Suggestion System              | Citizens can submit feedback and suggestions                                |
| 📅 Trash Schedule + Bins          | Bins and collection schedules viewable by all modules                       |
| 🧪 RESTful APIs + Swagger UI      | Full REST API exposed with interactive Swagger docs                         |

---

## 💡 My Role

- Led backend development of the entire system
- Designed and implemented the database model + REST API structure
- Created modular role-based access for system admin, driver, and citizen
- Delivered Swagger-based API documentation for internal and future use
- Ensured image upload handling and report validation logic

---

## 🧪 Deployment Details

- API runs on port `8083` by default
- Configurable in `application.properties`
- Future plans: Dockerize and expose through HTTPS proxy or Nginx

```properties
server.port=8083
spring.datasource.url=jdbc:mysql://localhost:3306/biskranadifa_database
spring.datasource.username=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

Base URL:   ```http://localhost:8083/```

Swagger UI: ```http://localhost:8083/swagger-ui/index.html#/```


## 📷 Image Gallery

## 🖼️ Biskra Nadifa – Image Gallery

Click on any image to zoom. All images are lazy-loaded for performance.


### 🖥️ Dashboard interfaces

![Login Page](../assets/images/blog/biskra-nadifa-1/login.png){width=300 loading=lazy }


![Dashboard](../assets/images/blog/biskra-nadifa-1/dashboard.png){ width=300 loading=lazy }


![Workflow 1](../assets/images/blog/biskra-nadifa-1/Screenshot_2025-06-19_09-27-13.png){ width=300 loading=lazy }


![Workflow 2](../assets/images/blog/biskra-nadifa-1/Screenshot_2025-06-19_09-27-32.png){ width=300 loading=lazy }

---

### 📱 Mobile Interface Screens

![Mobile 1](../assets/images/blog/biskra-nadifa-1/mobile1.png){ width=250 loading=lazy }

![Mobile 2](../assets/images/blog/biskra-nadifa-1/mobile2.png){ width=250 loading=lazy }

![Mobile 3](../assets/images/blog/biskra-nadifa-1/mobile3.png){ width=250 loading=lazy }

![Mobile 4](../assets/images/blog/biskra-nadifa-1/mobile4.png){ width=250 loading=lazy }




---

## 🔭 Future Work (Planned V2)

- Add JWT authentication + authorization per role

- Implement rate limiting and idempotency

- Add message queues (RabbitMQ or Kafka) for task creation and driver notification

- Build a driver-selection algorithm (based on distance or task load)

- Add Spring Boot Actuator + Micrometer for monitoring

- Dockerize and package the platform for deployment

- Add API pagination and image compression

- Write a technical article about API optimization