# HRMS Employee Lifecycle - QA Automation Demo

Demo implementation for **Scenario 2: HRMS Employee Lifecycle**
The assessment asks for a runnable automation project using POM, framework waits/auto-waiting, dynamic data, real assertions, logging/reporting, and a README. The workflow is Login → Create Employee → Search → Update → Verify Update → Delete → Search after deletion.

## Stack

- Java 17
- Maven
- Selenium WebDriver
- TestNG
- SLF4J Simple logging
- Page Object Model

## Project structure

```text
hrms-employee-lifecycle-demo/
├── pom.xml
├── testng.xml
├── README.md
├── .gitignore
└── src/test/java/com/dyad/hrms/
    ├── base/BaseTest.java
    ├── pages/LoginPage.java
    ├── pages/DashboardPage.java
    ├── pages/EmployeeListPage.java
    ├── pages/AddEmployeePage.java
    ├── pages/PersonalDetailsPage.java
    ├── tests/EmployeeLifecycleTest.java
    └── utils/TestData.java
```

## Prerequisites

1. JDK 17+
2. Maven 3.9+
3. Internet access for the demo site and Maven dependencies
4. Chrome installed

Selenium Manager is used, so a manually downloaded ChromeDriver is normally not required.

## Run

```bash
mvn clean test
```

Optional browser selection:

```bash
mvn clean test -Dbrowser=chrome
```

The test URL is configured in `BaseTest`.

## Test data

The employee first/middle/last names are generated with a timestamp. This avoids collisions between repeated executions.

The employee ID is **read from the application after creation** and stored for later search/update/delete operations. It is never hardcoded.

## Workflow implemented

1. Login as administrator.
2. Open PIM and create a new employee.
3. Capture the generated employee ID.
4. Search by the generated employee ID.
5. Update the employee's first and last name.
6. Verify the updated values.
7. Delete the employee.
8. Search again and assert that no employee record is returned.

## Assertions

The test contains real TestNG assertions for:

- generated employee ID is non-empty
- employee can be found after creation
- updated first/last name are displayed
- deleted employee is no longer returned

## Wait strategy

The framework uses Selenium explicit waits (`WebDriverWait` / ExpectedConditions). It intentionally does not use `Thread.sleep()`.

## Reporting

TestNG produces the standard report under:

```text
target/surefire-reports/
```

SLF4J logs are emitted during execution.

## Important assumption

The assessment source specifies the public OrangeHRM demo URL and the CRUD workflow, but does not provide credentials or exact UI selectors. This demo therefore uses the commonly provided OrangeHRM demo administrator credentials (`Admin` / `admin123`). If the public demo changes its credentials or UI, update the relevant values/selectors in `LoginPage` and page objects.

The source assessment specifically requires a working runnable project rather than a one-off script, POM, explicit/framework waits, dynamic data, real assertions, logging/reporting, and documentation.

## Git submission suggestion

Use incremental commits, for example:

```text
Initialize Maven/TestNG Selenium framework
Add Login and Dashboard page objects
Add Employee creation flow
Add dynamic employee search and verification
Add employee update validation
Add employee deletion validation
Add README and test reporting
```
