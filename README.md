# MediCare Hospital – Patient Admission System

A console-based, menu-driven Java application for managing patient records and bed allocation in a single 20-bed hospital ward (4 × 5 layout). I built this as a coursework exercise to practice object-oriented design, exception handling, in-memory state management, and unit testing. The project was developed using Apache NetBeans and built with Maven.

## Why I built it
I built this system to learn and demonstrate:
- Designing small multi-package Java applications (models, services, UI).
- Implementing input validation and checked exceptions for business rules.
- Managing application state in memory and writing focused unit tests (JUnit 5).
- Using an IDE workflow (Apache NetBeans) together with Maven for build/test cycles.

## What it does
- Register, view, update, and delete patient records.
- Allocate and release beds for inpatients in a 20-bed ward, enforcing allocation rules and preventing invalid operations (duplicate IDs, allocating occupied beds, allocating when full).
- Search and sort patients (by ID, surname) and produce simple reports/listings for the ward.
- Throw and handle checked exceptions (e.g., DuplicatePatientException, BedUnavailableException) to surface invalid operations.
- Include JUnit 5 unit tests that validate the core HospitalService behaviors.

## Tech / Stack
- Language: Java
- Required JDK: 17+
- Build: Maven (pom.xml)
- IDE used: Apache NetBeans
- Test framework: JUnit 5

## Project layout
```
hospital/
├── pom.xml
├── src/main/java/hospital/
│   ├── model/
│   │   ├── Patient.java          # base class
│   │   ├── Inpatient.java        # extends Patient, adds ward/bed info
│   │   ├── PatientCategory.java  # enum: INPATIENT, OUTPATIENT, EMERGENCY
│   │   └── Bed.java
│   ├── service/
│   │   ├── HospitalService.java  # core business logic
│   │   ├── DuplicatePatientException.java
│   │   └── BedUnavailableException.java
│   └── app/
│       └── Main.java             # console menu entry point
└── src/test/java/hospital/
    └── HospitalServiceTest.java  # JUnit 5 tests
```

## Requirements
- JDK 17 or later
- Maven 3.6+
- (Optional) Apache NetBeans to open and run the Maven project easily

## Build and run
From the project root:
```bash
cd hospital
mvn clean package
java -jar target/hospital-admission-system.jar
```

## Run the tests
```bash
mvn test
```

## Without Maven
If Maven isn't available, compile and run using the JDK directly:
```bash
cd hospital
mkdir out
javac -d out $(find src/main -name "*.java")
java -cp out hospital.app.Main
```
Note: the unit tests require JUnit 5 on the classpath (Maven supplies this automatically).

## Design notes
- Patient is the base class holding common fields (ID, name, age, gender, condition, category) and a display method.
- Inpatient extends Patient and adds wardNumber / bedNumber; only inpatients may be allocated beds.
- PatientCategory is an enum (INPATIENT, OUTPATIENT, EMERGENCY) used to enforce allocation rules.
- HospitalService manages application state in memory (Map for patients and List for beds) and throws checked exceptions for invalid operations.
- Main is a thin console/menu layer that calls HospitalService methods, keeping business logic separate from the UI.

## Developed with Apache NetBeans
To open the project in Apache NetBeans: File → Open Project → select the `hospital` folder (Maven `pom.xml` will be detected). Use NetBeans' Run and Test actions to build, run, and run the unit tests.

## Future improvements
- Persist patient and bed state to disk or a lightweight database instead of keeping everything in memory.
- Add integration tests for CLI flows and persistence.
- Improve CLI UX and add a non-interactive mode (command-line arguments or a REST API) for automation.
