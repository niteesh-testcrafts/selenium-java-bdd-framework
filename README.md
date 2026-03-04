What this is
End-to-end automation suite for OrangeHRM — an open source HR management platform. Built to demonstrate real-world automation patterns I use professionally: Page Object Model, BDD Cucumber, parallel execution, and CI/CD integration.
Covers four core modules: Login, Employee Management, Leave, and Recruitment.

Modules covered
ModuleScenariosLoginValid login, invalid credentials, empty fields, forgot password, logoutEmployeeAdd employee, search by name, no results, scenario outline with multiple employeesLeaveApply leave, leave list, date/type selectionRecruitmentAdd vacancy, candidate search, results validation

How it's structured
orangehrm-automation/
├── src/
│   ├── main/java/com/automation/
│   │   ├── config/
│   │   │   ├── ConfigReader.java       ← reads config.properties
│   │   │   └── DriverFactory.java      ← thread-safe WebDriver (ThreadLocal)
│   │   └── utils/
│   │       ├── WaitUtils.java          ← all explicit waits in one place
│   │       └── ScreenshotUtils.java    ← captures screenshots on failure
│   └── test/java/com/automation/
│       ├── pages/
│       │   ├── BasePage.java           ← shared actions (click, type, scroll...)
│       │   ├── login/
│       │   │   ├── LoginPage.java
│       │   │   └── DashboardPage.java
│       │   ├── employee/
│       │   │   ├── EmployeeListPage.java
│       │   │   └── AddEmployeePage.java
│       │   ├── leave/
│       │   │   └── LeavePage.java
│       │   └── recruitment/
│       │       └── RecruitmentPage.java
│       ├── stepdefs/
│       │   ├── Hooks.java              ← @Before/@After with screenshot on fail
│       │   ├── LoginSteps.java
│       │   ├── EmployeeSteps.java
│       │   ├── LeaveSteps.java
│       │   └── RecruitmentSteps.java
│       └── runners/
│           └── TestRunner.java         ← Cucumber + TestNG entry point
│   └── test/resources/
│       ├── features/
│       │   ├── login/Login.feature
│       │   ├── employee/Employee.feature
│       │   ├── leave/Leave.feature
│       │   └── recruitment/Recruitment.feature
│       ├── config.properties           ← base URL, credentials, timeouts
│       └── testng.xml                  ← parallel execution config
├── pom.xml
└── README.md

Running the tests
Make sure you have Java 11+, Maven 3.8+, and Chrome installed. The framework auto-manages ChromeDriver via WebDriverManager — no manual driver setup needed.
bash# clone and enter the project
git clone https://github.com/niteesh_qa/orangehrm-automation.git
cd orangehrm-automation

# run everything
mvn clean test

# run by tag
mvn clean test -Dcucumber.filter.tags="@smoke"
mvn clean test -Dcucumber.filter.tags="@login"
mvn clean test -Dcucumber.filter.tags="@employee"
mvn clean test -Dcucumber.filter.tags="@leave"
mvn clean test -Dcucumber.filter.tags="@recruitment"

# run headless (great for CI)
mvn clean test -Dheadless=true

# run on a different browser
mvn clean test -Dbrowser=firefox

# open allure report after run
mvn allure:serve

Target application
OrangeHRM Demo: https://opensource-demo.orangehrmlive.com
Username: Admin
Password: admin123
This is a publicly available demo — credentials are the same for everyone and data resets periodically.

Design decisions worth mentioning
ThreadLocal for drivers — every thread gets its own WebDriver instance, so parallel test execution works without tests interfering with each other.
WaitUtils as a single source of truth — instead of sprinkling Thread.sleep() or WebDriverWait everywhere, all waits go through WaitUtils. Makes it easy to tune timeouts in one place.
Screenshots on failure — Hooks.java captures a screenshot whenever a scenario fails and attaches it to both the Cucumber HTML report and Allure. Saves a lot of debugging time.
Custom dropdown handler in BasePage — OrangeHRM uses Vue.js custom dropdowns that don't work with Selenium's native Select class. selectDropdownByText() handles this properly.

A bit about me
I'm Niteesh Anantha, a QA Automation Engineer based in Chennai. This is one of several automation projects I've built to practice and showcase real-world testing patterns.
📧 niteesh.anantha@gmail.com
🔗 linkedin.com/in/niteesh09

License
MIT — use it however you like.
