
# Spring PetClinic – Jenkins CI/CD Demo

This repository is a fork of the **Spring PetClinic** sample application, enhanced with a **Jenkins Pipeline** to automate **Build → Test → Deploy**.

---

## Project Overview

Spring PetClinic is a simple Java Spring Boot application that demonstrates:

- Spring Boot with JPA (Hibernate)
- H2 in-memory database
- REST endpoints and web UI
- Unit and integration tests

---

## Jenkins Pipeline (Jenkinsfile)

The pipeline automates the following stages:

1. **Checkout**  
   Pulls the code from this repository.

2. **Build**  
   Uses the Maven wrapper (`./mvnw`) to build the project and package it into a `.jar`.  
   Command used:  
   ```bash
   chmod +x mvnw
   ./mvnw clean package -DskipTests


3. **Test**
   Runs the unit and integration tests. Test results are published in Jenkins using `junit`.
   Command used:

   ```bash
   ./mvnw test
 

4. **Deploy**
   Starts the Spring Boot application in the background on port `9999`. Logs are saved to `app.log`.
   Command used:

   ```bash
   nohup java -jar target/*.jar --server.port=9999 > app.log 2>&1 &
   ```

---

## How to Use

1. Clone the repository:

   ```bash
   git clone https://github.com/abd-elrahman-mohamed-anter/spring-petclinic-fork.git
   cd spring-petclinic-fork
   ```

2. Ensure `mvnw` is executable:

   ```bash
   chmod +x mvnw
   ```

3. Run manually (optional):

   ```bash
   ./mvnw clean package -DskipTests
   nohup java -jar target/spring-petclinic-3.5.0-SNAPSHOT.jar --server.port=9999 > app.log 2>&1 &
   ```

4. Access the app in the browser:

   ```
   http://localhost:9999
   ```

---

## Notes

* The application uses an **in-memory H2 database** by default. All data is lost when the app stops.
* Jenkins Pipeline allows **CI/CD automation** for building, testing, and deploying the app.
* Port conflicts may occur if multiple instances are running (default Spring Boot port is `8080`).

---

## References

* [Spring PetClinic GitHub](https://github.com/spring-projects/spring-petclinic)
* [Spring Boot Documentation](https://spring.io/projects/spring-boot)
* [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)
