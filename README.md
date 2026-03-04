# OrangeHRM Selenium Automation Framework

![Java](https://img.shields.io/badge/Java-11+-orange?style=flat-square&logo=java)
![Selenium](https://img.shields.io/badge/Selenium-4.x-green?style=flat-square&logo=selenium)
![Cucumber](https://img.shields.io/badge/Cucumber-BDD-brightgreen?style=flat-square&logo=cucumber)
![TestNG](https://img.shields.io/badge/TestNG-7.x-red?style=flat-square)
![Maven](https://img.shields.io/badge/Maven-Build-blue?style=flat-square&logo=apache-maven)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

---

## What this is

End-to-end automation suite for [OrangeHRM](https://opensource-demo.orangehrmlive.com) built to demonstrate real-world automation patterns: Page Object Model, BDD Cucumber, parallel execution, and CI/CD integration.

Covers four core modules: **Login**, **Employee Management**, **Leave**, and **Recruitment**.

---

## Modules covered

| Module | Scenarios |
|---|---|
| Login | Valid login, invalid credentials, empty fields, forgot password, logout |
| Employee | Add employee, search by name, no results, scenario outline |
| Leave | Apply leave, leave list, date and type selection |
| Recruitment | Add vacancy, candidate search, results validation |

---

## Project structure

```
orangehrm-automation/
├── src/main/java/com/automation/
│   ├── config/
│   │   ├── ConfigReader.java
│   │   └── DriverFactory.java
│   └── utils/
│       ├── WaitUtils.java
│       └── ScreenshotUtils.java
├── src/test/java/com/automation/
│   ├── pages/
│   │   ├── BasePage.java
│   │   ├── login/LoginPage.java
│   │   ├── login/DashboardPage.java
│   │   ├── employee/EmployeeListPage.java
│   │   ├── employee/AddEmployeePage.java
│   │   ├── leave/LeavePage.java
│   │   └── recruitment/RecruitmentPage.java
│   ├── stepdefs/
│   │   ├── Hooks.java
│   │   ├── LoginSteps.java
│   │   ├── EmployeeSteps.java
│   │   ├── LeaveSteps.java
│   │   └── RecruitmentSteps.java
│   └── runners/
│       └── TestRunner.java
├── src/test/resources/
│   ├── features/
│   │   ├── login/Login.feature
│   │   ├── employee/Employee.feature
│   │   ├── leave/Leave.feature
│   │   └── recruitment/Recruitment.feature
│   ├── config.properties
│   └── testng.xml
├── pom.xml
└── README.md
```

---

## Running the tests

Requires Java 11+, Maven 3.8+, and Chrome. ChromeDriver is managed automatically via WebDriverManager.

```bash
# clone the repo
git clone https://github.com/niteesh_qa/orangehrm-automation.git
cd orangehrm-automation

# run all tests
mvn clean test

# run by module
mvn clean test -Dcucumber.filter.tags="@smoke"
mvn clean test -Dcucumber.filter.tags="@login"
mvn clean test -Dcucumber.filter.tags="@employee"
mvn clean test -Dcucumber.filter.tags="@leave"
mvn clean test -Dcucumber.filter.tags="@recruitment"

# headless mode
mvn clean test -Dheadless=true

# different browser
mvn clean test -Dbrowser=firefox

# view allure report
mvn allure:serve
```

---

## Target app

**URL:** https://opensource-demo.orangehrmlive.com

```
Username: Admin
Password: admin123
```

Public demo site — credentials are shared and data resets periodically.

---

## Design decisions

**ThreadLocal drivers** — each thread gets its own WebDriver so parallel runs don't clash.

**WaitUtils** — all explicit waits in one class instead of scattered `Thread.sleep()` calls.

**Screenshots on failure** — `Hooks.java` auto-captures and attaches to both Cucumber and Allure reports.

**Custom dropdown handler** — OrangeHRM uses Vue.js dropdowns that break Selenium's native `Select`. `selectDropdownByText()` in `BasePage` handles this correctly.

---

## About me

I'm **Niteesh Anantha**, a QA Automation Engineer based in Chennai.

📧 niteesh.anantha@gmail.com
🔗 [linkedin.com/in/niteesh09](https://linkedin.com/in/niteesh09)

---

## License

MIT — use it however you like.
