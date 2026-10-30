# Automation Exercise Selenium Tests

A Java-based UI automation suite for [Automation Exercise](https://automationexercise.com/). The project uses Selenium WebDriver with Firefox, TestNG, Maven, Page Object Model (POM), WebDriverManager, and JavaFaker.

## What is covered

The suite contains 26 TestNG test classes covering common e-commerce workflows, including:

- User registration, duplicate-email validation, login, invalid login, and logout
- Contact-us form and test-cases page validation
- Product listing, product details, search, categories, brands, and reviews
- Adding one or multiple products to the cart
- Quantity validation and product removal
- Checkout, address details, payment validation, and invoice download
- Recommended products
- Subscription validation on the home and cart pages
- Scrolling to the top using the arrow and without the arrow

Test classes are located in [`src/test/java/tests`](C:/WorkSpace/automationExercise-Automation/src/test/java/tests), with page objects in [`src/test/java/pages`](C:/WorkSpace/automationExercise-Automation/src/test/java/pages).

## Technology stack

- Java
- Maven
- Selenium WebDriver `4.31.0`
- TestNG `7.11.0`
- WebDriverManager `5.7.0`
- JavaFaker `1.0.2`
- Firefox / geckodriver

## Prerequisites

1. Install a supported JDK and Maven.
2. Install Mozilla Firefox.
3. Ensure the machine can access `https://automationexercise.com/`.
4. Use a network connection on the first run so Maven can download dependencies and WebDriverManager can resolve geckodriver.

The current test setup creates a Firefox driver, maximizes the browser, applies a 10-second implicit wait, and opens the Automation Exercise home page before each test. The browser is closed after each test.

## Running the tests

From the project root:

```bash
mvn clean test
```

To run the suite using the TestNG XML file:

```bash
mvn test -Dsurefire.suiteXmlFiles=src/test/java/MyTests.xml
```

> The Java test classes extend `tools.BaseTest`, which contains the common browser setup and teardown. If the XML suite does not match the current test class names, run the standard Maven command or update [`MyTests.xml`](C:/WorkSpace/automationExercise-Automation/src/test/java/MyTests.xml) before using the XML command.

## Project structure

```text
automationExercise-Automation/
├── pom.xml
├── src/
│   ├── main/java/
│   │   └── selenium_Package/Automation_Project/App.java
│   └── test/java/
│       ├── pages/       # Page Object Model classes
│       ├── tests/       # TestNG test cases
│       ├── tools/       # Shared test/page utilities and base classes
│       └── MyTests.xml  # TestNG suite configuration
├── target/              # Maven build output (generated)
└── test-output/         # TestNG reports (generated)
```

### Main support classes

- [`BaseTest.java`](C:/WorkSpace/automationExercise-Automation/src/test/java/tools/BaseTest.java): starts and closes Firefox for each test.
- [`BasePage.java`](C:/WorkSpace/automationExercise-Automation/src/test/java/tools/BasePage.java): shared waits, scrolling, resilient clicks, and ad removal helpers.
- Page classes such as [`HomePage.java`](C:/WorkSpace/automationExercise-Automation/src/test/java/pages/HomePage.java), [`ProductPage.java`](C:/WorkSpace/automationExercise-Automation/src/test/java/pages/ProductPage.java), and [`CheckOutPage.java`](C:/WorkSpace/automationExercise-Automation/src/test/java/pages/CheckOutPage.java): encapsulate page locators and actions.

## Reports

After a test run, TestNG output is written to [`test-output`](C:/WorkSpace/automationExercise-Automation/test-output). Useful files include:

- [`emailable-report.html`](C:/WorkSpace/automationExercise-Automation/test-output/emailable-report.html): summary report
- [`index.html`](C:/WorkSpace/automationExercise-Automation/test-output/index.html): navigable TestNG report
- `testng-results.xml`: machine-readable results
- `junitreports/`: JUnit-format result files

These files are generated artifacts and may be replaced by the next test run.

## Notes and limitations

- Tests run against a live external website, so availability, network conditions, advertisements, and site changes can affect results.
- The suite currently runs on Firefox because `BaseTest` constructs a `FirefoxDriver`.
- Some tests create data dynamically with JavaFaker; tests that exercise existing-user or existing-email behavior may rely on data already present on the target site.
- Credentials, payment details, and other test data should be supplied only for test accounts and must not be committed to the repository.
- The project does not currently expose configurable browser or base-URL properties; update `BaseTest.java` if environment-specific configuration is required.

## License

No license file is currently included. Add an appropriate license before distributing the project.
