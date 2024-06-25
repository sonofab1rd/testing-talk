---
# try also 'default' to start simple
theme: default
favicon: "beaker_6787266.png"
# some information about your slides, markdown enabled
title: Software Testing
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

<h1>Software Testing</h1>

<h2>The best talk in the world about Software Testing!</h2>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->
---
title: What is Software Testing 
---

<h1>What is Software Testing?</h1>

<li class="text-sm">The process of evaluating and verifying that a software product or application does what it’s intended to do. 
  <sup>1</sup>
</li> 

<h3 class="mt-2" v-click> Why should I test? </h3>
  <li v-click>To make sure what you've written does what you intended.</li>
  <li v-click>To make sure you haven't broken some other functionality.</li>
  <li v-click>To speed up the development processs.</li>
  <li v-click>To improve your confidence.</li>
  <li v-click>As part of the refactoring process.</li>

<h3 v-click>What are some common types?</h3>
  <li v-click>Unit Tests</li>
  <li v-click>Integration Tests</li>
  <li v-click> End to End Tests</li>
  <li v-click> Component Tests</li>
  <li v-click> Benchmarking Tests</li>
  <li v-click> Reliablility</li>

<span>1:<a href="https://www.ibm.com/topics/software-testing">https://www.ibm.com/topics/software-testing</a></span>

---

<h1>What are some testing tools?</h1>
<div></div>
<p>Browser
  <li>Cypress</li>
  <li>Playwright</li>
  <li>Selenium</li>
</p>
<p>Framework
  <li>Junit</li>
  <li>Mockito</li>
</p>
<p>Misc
  <li>Java Profiler</li>
</p>

---

<h1>Cypress</h1>

<h4>Install Cypress</h4>

<li>create a cypress-talk folder</li>

```bash {0|all}
mkdir cypress-talk
cd cypress-talk
```

<li>initialize with npm</li>

```bash {0|1}
npm init
```

<li>enter through all the prompts</li>
<li>add cypress</li>

```bash {0|1}
npm install cypress --save-dev
```

<li>open cypress</li>

```bash {0|1}
npx cypress open
```

---

<h4>Install Cypress cont'd</h4>

<li>click End To End testing config option</li>
<li>review added files</li>
<li>click to continue</li>
<li>Chrome Selected by default</li>
<li>click Start E2E testing in chrome</li>
<li>click scaffold example specs</li>
<li>click ok!</li>
<li>under 1 getting started</li>
<li>click todo to run the todo test</li>

---

<h1>What just happened?</h1>

<li>Cypress opened up a webpage with a todo list, started getting elements on the page and asserting things about them, and listed out the results to the left.</li>

<h3 class="ma-2">How does it work?</h3>

<h4>In a nutshell...</h4>

<li>Built with JavaScript/Node</li>
<li>Runs directly in the browser</li>
<li>Able to interact directly with the page</li>
<li>Different from Selenium. Which, must send requests to the page.</li>

<a href="https://www.cypress.io/how-it-works">More details here.</a>

---

<h1>todo.cy.js</h1>

<pre class="text-size-xs pb-2">
cypress-talk
├── cypress
└── e2e
    └── 1-getting-started
        └── todo.cy.js
</pre>
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
  });

  it("displays two todo items by default", () => {
    cy.get(".todo-list li").should("have.length", 2);
    cy.get(".todo-list li").first().should("have.text", "Pay electric bill");
    cy.get(".todo-list li").last().should("have.text", "Walk the dog");
  });
...
```
---

<h1>todo.cy.js</h1>

<span>The breakdown</span>

````md magic-move
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
  });
```
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
    // Visit a remote url
  });
```
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
    // Visit a remote url
  });

  it("displays two todo items by default", () => {
    cy.get(".todo-list li").should("have.length", 2);
    cy.get(".todo-list li").first().should("have.text", "Pay electric bill");
    cy.get(".todo-list li").last().should("have.text", "Walk the dog");
  });
```
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
    // Visit a remote url
  });

  it("displays two todo items by default", () => {
    cy.get(".todo-list li").should("have.length", 2);
    // Get one or more DOM elements
    cy.get(".todo-list li").first().should("have.text", "Pay electric bill");
    cy.get(".todo-list li").last().should("have.text", "Walk the dog");
  });
```
```js
describe("example to-do app", () => {
  beforeEach(() => {
    cy.visit("https://example.cypress.io/todo");
    // Visit a remote url
  });

  it("displays two todo items by default", () => {
    cy.get(".todo-list li").should("have.length", 2);
    // Get one or more DOM elements
    // Should creates an Assertion
    // One of the most common first arguments is
    // any valid chainer that comes from Chai or Chai-jQuery or Sinon-Chai.
    // With the second argument being the expected value.
    cy.get(".todo-list li").first().should("have.text", "Pay electric bill");
    cy.get(".todo-list li").last().should("have.text", "Walk the dog");
  });
```
````
<!-- <span v-click>More information about assertions/chainers <a href="https://docs.cypress.io/guides/references/assertions">here</a></span>
<p></p>
<span v-click>More information about jest <a href="https://jestjs.io/">here</a></span> -->
<!-- You may want to talk briefly about jest here. -->

---

<iframe src="https://docs.cypress.io/guides/references/assertions" title="Cypress Assertion Docs" height="500" width="800"></iframe>
 

---

<h1>A (more) real Cypress example</h1>

<a href="https://gitlab.openpracticesolutions.com/openpm/testing/cypress-openpm">cypress-openpm</a>

<pre class="text-size-xs pb-2">
cypress-openpm
└── cypress
    ├── downloads
    └── e2e
        └── test
            └── openpm
                ├── 00_RESETS
                └── 01_Login_Screen
                    ├── 01_C3852_Access_Login_and_Verify_Content.cy.js
                    ├── 02_C3854_Login_Verify_Required_Info.cy.js
                    ├── 03_C3853_Login_Show_Password.cy.js
                    └── 04_C215_Login_No_2_Factor.cy.js
</pre>

---

<h4>04_C215_Login_No_2_Factor.cy.js</h4>

````md magic-move
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();
```

```js
//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
````
----
<h4>04_C215_Login_No_2_Factor.cy.js</h4>

````md magic-move
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  // Named to match the TestRail test case.
  // Allows us to send the test results to test rail, 
  // matching to case automatically.
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
    // Since we login before all the tests,
    // it makes sense to make it a reusable function.
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
    // How did it just go to OpenPM?
    // We only have a slash here!
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    // When you get an input, you can type into it!
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    // You can also click buttons!
    cy.wait(1000);
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
```js
import { loginNo2Factor } from "./Login_Functions.cy";

export function C215() {
  describe("[C215] Login No 2 Factor", () => {
    loginNo2Factor();
  });
}
C215();

//User with No 2 Factor Authentication
function loginNo2Factor() {
  it("Opens OpenPM Website", () => {
    cy.visit("/");
  });
  it("Signs into OpenPM", () => {
    cy.get("#id").type("actual user name here");
    cy.get("#id").should("have.value", "actual user name here");
    cy.get("#up").type("actual password here");
    cy.get("#up").should("have.value", "actual password here");
    cy.get("#logBut").click();
    cy.wait(1000);
    // Cypress waits automatically.
    // Sometimes you need to wait a little longer.
    cy.get("#header_table").should("include.text", "Home Dashboard");
    cy.url().should("include", "/topenpm.jcm");
  });
}
```
````

---

<h1>Cypress Recap</h1>

<h4>So far we've covered the basics of Cypress and E2E testing!</h4>

<li>Installed Cypress</li>
<li>Ran a sample test</li>
<li>Covered the basics: visit, get and should(assertions)</li>
<li>Ran a real test</li>
<li>Learned about more features: type, click and wait</li>

---

<h1>Unit Tests!</h1>

<h4>JUnit</h4>

<span>Instead of testing from top to bottom. Let's test individual units of functionality.</span>

<a href="https://junit.org/junit5/docs/current/user-guide/">JUnit Docs</a>

<iframe src="https://junit.org/junit5/docs/current/user-guide/" title="JUnit Docs" height="300" width="800"></iframe>

---

<h4>JUnit</h4>

<p>Some prereq's...</p>
<p>You'll need a JDK</p>
```bash {1|2|3|0}
curl -s "https://get.sdkman.io" | bash
sdk install java 21.0.2-tem
sdk use java 21.0.2-tem
```
<p>You'll need maven to build it.</p>
```bash {0|1|2|0}
sdk install maven 3.9.8
sdk use maven 3.9.8
```
<p>You'll need a project with a JUnit dependency</p>
<a href="https://github.com/junit-team/junit5-samples/tree/r5.10.2/junit5-jupiter-starter-maven">junit5-jupiter-starter-maven project</a>

```bash {0|1}
git clone https://github.com/junit-team/junit5-samples.git
```

<p>Good luck with your IDE...</p>

---

<h4>JUnit</h4>

<p>We can do it with no IDE!</p>

```bash {1|2|3}
cd junit5-samples/junit5-jupiter-starter-maven
mvn clean install
mvn surefire-report:report
```

<p>From the current directory, you'll now have a test report at /target/site/surefire-report.html</p>
<p>Open it in your browser!</p>

---
 
<h4>JUnit</h4>

<p>This project has a Calculator class and a CalculatorTests class.</p>
<p>Running the Calculator tests yields some familiar output!</p>
<pre>
✔️ CalulatorTests
  ✔️ 1 + 1 = 2
  ✔️ add(int, int, int)
    ✔️ 0 + 1 = 1
    ✔️ 1 + 2 = 3
    ✔️ 49 + 51 = 100
    ✔️ 1 + 100 = 101
</pre>

---

<h4>JUnit</h4>

````md magic-move
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
  // Basic @Test Annotation
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
  // Changes the name of the test in the test result display!
  // Otherwise the method name will be used.
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
    // All Tests are package-private and void.
    // This allows the test runner easy access to the tests. 
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
    // basic assert method provided by JUnit
    // First arg is expected value.
    // Second is actual value.
    // Third is the message to display in case of failed test.
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
  // You can give your tests parameters!
  // In this case we set the display name using a string
  // with the parameter values interpolated. {0} represents the first arg
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
```java
class CalculatorTests {

	@Test
	@DisplayName("1 + 1 = 2")
	void addsTwoNumbers() {
		Calculator calculator = new Calculator();
		assertEquals(2, calculator.add(1, 1), "1 + 1 should equal 2");
	}

	@ParameterizedTest(name = "{0} + {1} = {2}")
	@CsvSource({
			"0,    1,   1",
			"1,    2,   3",
			"49,  51, 100",
			"1,  100, 101"
	})
  // We can supply a static list of arguments using CsvSource!
	void add(int first, int second, int expectedResult) {
		Calculator calculator = new Calculator();
		assertEquals(expectedResult, calculator.add(first, second),
				() -> first + " + " + second + " should equal " + expectedResult);
	}
}
```
````

---

<h4>JUnit</h4>

```java {all}{maxHeight:'400px'}
class DateParserTest {
	Date validDOBDate = null;
	Date validDate = null;

	@BeforeEach
	void init() {
		DateTimeFormatter format = DateTimeFormatter.BASIC_ISO_DATE;
		validDOBDate = Date.valueOf(LocalDate.parse("19990101", format));
		format = DateTimeFormatter.BASIC_ISO_DATE;
		validDate = Date.valueOf(LocalDate.parse("20990101", format));

	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 2099", "" })
	void nonDOBInvalid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertNull(parsedDate);
	}

	@Test
	void nullNonDOB() {
		Date parsedDate = DateParser.parse(null);
		assertNull(parsedDate);
	}

	@Test
	void nullDOB() {
		Date parsedDate = DateParser.parseDOB(null);
		assertNull(parsedDate);
	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 1999", "" })
	void dobInvalid(String input) {
		Date parsedDate = DateParser.parseDOB(input);
		assertNull(parsedDate);
	}

	void dobInvalid() {
		Date parsedDate = DateParser.parseDOB(null);
		assertNull(parsedDate);
	}

	void nonDOBInvalid() {
		Date parsedDate = DateParser.parse(null);
		assertNull(parsedDate);
	}

	@ParameterizedTest
	@ValueSource(strings = { "01/01/99", "01/01/1999", "01-01-1999", "1-1-1999", "1/1/99", "1999-01-01", "01011999",
			"19990101", "1/1/1999", "1/01/1999", "10199", "01 01 99" })
	void dobValid(String input) {
		Date parsedDate = DateParser.parseDOB(input);
		assertEquals(validDOBDate, parsedDate);
	}

	@ParameterizedTest
	@ValueSource(strings = { "01/01/99", "01/01/2099", "01-01-2099", "1-1-2099", "1/1/99", "2099-01-01", "01012099",
			"20990101", "1/1/2099", "1/01/2099", "10199", "01 01 99" })
	void nonDOBValid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertEquals(validDate, parsedDate);
	}

}
```

---

<h4>JUnit</h4>

````md magic-move
```java
class DateParserTest {
	Date validDOBDate = null;
	Date validDate = null;

	@BeforeEach
	void init() {
		DateTimeFormatter format = DateTimeFormatter.BASIC_ISO_DATE;
		validDOBDate = Date.valueOf(LocalDate.parse("19990101", format));
		format = DateTimeFormatter.BASIC_ISO_DATE;
		validDate = Date.valueOf(LocalDate.parse("20990101", format));

	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 2099", "" })
	void nonDOBInvalid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertNull(parsedDate);
	}
...
}
```
```java
class DateParserTest {
  //Some helper fields
	Date validDOBDate = null;
	Date validDate = null;

	@BeforeEach
	void init() {
		DateTimeFormatter format = DateTimeFormatter.BASIC_ISO_DATE;
		validDOBDate = Date.valueOf(LocalDate.parse("19990101", format));
		format = DateTimeFormatter.BASIC_ISO_DATE;
		validDate = Date.valueOf(LocalDate.parse("20990101", format));

	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 2099", "" })
	void nonDOBInvalid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertNull(parsedDate);
	}
...
```
```java
class DateParserTest {
	Date validDOBDate = null;
	Date validDate = null;

	@BeforeEach
  // We have some Lifecycle hooks
  // @BeforeEach, @AfterEach, @BeforeAll, @AfterAll
  // @BeforeEach runs the annotated method before every test.
  // @AfterEach runs the annotated method after every test.
  // @BeforeAll runs the annotated method once, before any of the tests are run.
  // @AfterAll runs the annotated method once, after all the tests have run.
	void init() {
		DateTimeFormatter format = DateTimeFormatter.BASIC_ISO_DATE;
		validDOBDate = Date.valueOf(LocalDate.parse("19990101", format));
		format = DateTimeFormatter.BASIC_ISO_DATE;
		validDate = Date.valueOf(LocalDate.parse("20990101", format));

	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 2099", "" })
	void nonDOBInvalid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertNull(parsedDate);
	}
...
```
```java
class DateParserTest {
	Date validDOBDate = null;
	Date validDate = null;

	@BeforeEach
	void init() {
		DateTimeFormatter format = DateTimeFormatter.BASIC_ISO_DATE;
		validDOBDate = Date.valueOf(LocalDate.parse("19990101", format));
		format = DateTimeFormatter.BASIC_ISO_DATE;
		validDate = Date.valueOf(LocalDate.parse("20990101", format));

	}

	@ParameterizedTest
	@ValueSource(strings = { "ABC", "01 01 2099", "" })
   // @ValueSource lets us provide an array of values to a single parameter. 
   // The test will run once for each value.
	void nonDOBInvalid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertNull(parsedDate);
	}
...
}
```
```java
class DateParserTest {
	
  ...	
  // The last two test cases.

	@ParameterizedTest
	@ValueSource(strings = { "01/01/99", "01/01/1999", "01-01-1999", "1-1-1999", "1/1/99", "1999-01-01", "01011999",
			"19990101", "1/1/1999", "1/01/1999", "10199", "01 01 99" })
	void dobValid(String input) {
		Date parsedDate = DateParser.parseDOB(input);
		assertEquals(validDOBDate, parsedDate);
	}

	@ParameterizedTest
	@ValueSource(strings = { "01/01/99", "01/01/2099", "01-01-2099", "1-1-2099", "1/1/99", "2099-01-01", "01012099",
			"20990101", "1/1/2099", "1/01/2099", "10199", "01 01 99" })
	void nonDOBValid(String input) {
		Date parsedDate = DateParser.parse(input);
		assertEquals(validDate, parsedDate);
	}

}
```
````

---

<h4>JUnit</h4>

````md magic-move
```java
@ExtendWith({ OPSIntegrationTestExtension.class, DBParameterResolver.class })
class HL7InIT {
	int testInterfaceFileRowid = 0;
	int testInterfaceInRowid = 0;
	String testInterfaceUserid = "";
	int HIGH_PRIORITY = 1;
	HL7In hl7In;
	InterfaceFile interfaceFile;

	@Test
	void processHL7(DataBase db) throws Exception {
		Connection conn = db.getConnection();
		PreparedStatement ps = conn.prepareStatement("SELECT * FROM updocm.interface WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		ResultSet rs = ps.executeQuery();
		rs.next();
		...
	}
  ...
}
```
```java
@ExtendWith({ OPSIntegrationTestExtension.class, DBParameterResolver.class })
//We'll take a look at the extensions next.
class HL7InIT {
	int testInterfaceFileRowid = 0;
	int testInterfaceInRowid = 0;
	String testInterfaceUserid = "";
	int HIGH_PRIORITY = 1;
	HL7In hl7In;
	InterfaceFile interfaceFile;

	@Test
	void processHL7(DataBase db) throws Exception {
		Connection conn = db.getConnection();
		PreparedStatement ps = conn.prepareStatement("SELECT * FROM updocm.interface WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		ResultSet rs = ps.executeQuery();
		rs.next();
		...
	}
  ...
}
```
```java
@ExtendWith({ OPSIntegrationTestExtension.class, DBParameterResolver.class })
class HL7InIT {
	...

	@Test
	void processHL7(DataBase db) throws Exception {
    // The DBParameterResolver controlls the DataBase parameter that is passed in.
		Connection conn = db.getConnection();
		PreparedStatement ps = conn.prepareStatement("SELECT * FROM updocm.interface WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		ResultSet rs = ps.executeQuery();
		rs.next();
		HL7Data.Interface thisInterface = new HL7Data.Interface(rs);
		ps = conn.prepareStatement("SELECT * FROM updocm.interface_settings WHERE userid = ?");
		...
	}
  ...
}
```
```java
@ExtendWith({ OPSIntegrationTestExtension.class, DBParameterResolver.class })
class HL7InIT {
	...

	@Test
	void processHL7(DataBase db) throws Exception {
		Connection conn = db.getConnection();
    // With that connection we can get whatever we need from the DB!
		PreparedStatement ps = conn.prepareStatement("SELECT * FROM updocm.interface WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		ResultSet rs = ps.executeQuery();
		rs.next();
		HL7Data.Interface thisInterface = new HL7Data.Interface(rs);
		ps = conn.prepareStatement("SELECT * FROM updocm.interface_settings WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		rs = ps.executeQuery();
		rs.next();
		thisInterface.settings = new HL7Data.InterfaceGlobalSettings(rs);
		ps = conn.prepareStatement("SELECT * FROM updocm.interface_in WHERE rowid = ?");
		ps.setInt(1, testInterfaceInRowid);
		rs = ps.executeQuery();
		rs.next();
		HL7In.InterfaceIn in = new HL7In.InterfaceIn(rs);
		HL7In.process(thisInterface, in, 1);
	}
  ...
}
```
```java
@ExtendWith({ OPSIntegrationTestExtension.class, DBParameterResolver.class })
class HL7InIT {
	...

	@Test
	void processHL7(DataBase db) throws Exception {
		Connection conn = db.getConnection();
		PreparedStatement ps = conn.prepareStatement("SELECT * FROM updocm.interface WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		ResultSet rs = ps.executeQuery();
		rs.next();
		HL7Data.Interface thisInterface = new HL7Data.Interface(rs);
		ps = conn.prepareStatement("SELECT * FROM updocm.interface_settings WHERE userid = ?");
		ps.setString(1, testInterfaceUserid);
		rs = ps.executeQuery();
		rs.next();
		thisInterface.settings = new HL7Data.InterfaceGlobalSettings(rs);
		ps = conn.prepareStatement("SELECT * FROM updocm.interface_in WHERE rowid = ?");
		ps.setInt(1, testInterfaceInRowid);
		rs = ps.executeQuery();
		rs.next();
		HL7In.InterfaceIn in = new HL7In.InterfaceIn(rs);
		HL7In.process(thisInterface, in, 1);
	}
  ...
}
```
````

---

<h4>JUnit</h4>

````md magic-move
```java
public class OPSIntegrationTestExtension implements BeforeAllCallback {
    public static final String TEST_DB = "updoc01";
    private static final DataBase db = connectDB.getDB();

    @Override
    public void beforeAll(ExtensionContext extensionContext) {
        setDb();
        SQL.map.put(Thread.currentThread(), db);
    }

    private static void setDb(){
        assert db != null;
        db.useDB(TEST_DB);
        db.setDbId(TEST_DB.replace("updoc", ""));
    }
}
```
```java
public class OPSIntegrationTestExtension implements BeforeAllCallback {
  // Other Callback classes are also available. e.g. BeforeEach, AfterEach, AfterAll
    public static final String TEST_DB = "updoc01";
    private static final DataBase db = connectDB.getDB();

    @Override
    public void beforeAll(ExtensionContext extensionContext) {
        setDb();
        SQL.map.put(Thread.currentThread(), db);
    }

    private static void setDb(){
        assert db != null;
        db.useDB(TEST_DB);
        db.setDbId(TEST_DB.replace("updoc", ""));
    }
}
```
```java
public class OPSIntegrationTestExtension implements BeforeAllCallback {
    public static final String TEST_DB = "updoc01";
    private static final DataBase db = connectDB.getDB();

    @Override
    public void beforeAll(ExtensionContext extensionContext) {
      // This is called prior to any tests being run.
      // It allows us access to the DB and the abililty to use
      // OpsEntities in tests.
        setDb();
        SQL.map.put(Thread.currentThread(), db);
    }

    private static void setDb(){
        assert db != null;
        db.useDB(TEST_DB);
        db.setDbId(TEST_DB.replace("updoc", ""));
    }
}
```
````

---

<h4>JUnit</h4>

````md magic-move
```java
public class DBParameterResolver implements ParameterResolver {
    @Override
    public boolean supportsParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        return parameterContext.getParameter().getType().equals(DataBase.class);
    }

    @Override
    public Object resolveParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        return SQL.getCurrentDataBase();
    }
}
```
```java
public class DBParameterResolver implements ParameterResolver {
    @Override
    public boolean supportsParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        //validates the type of parameter that is passed in.
        return parameterContext.getParameter().getType().equals(DataBase.class);
    }

    @Override
    public Object resolveParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        return SQL.getCurrentDataBase();
    }
}
```
```java
public class DBParameterResolver implements ParameterResolver {
    @Override
    public boolean supportsParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        return parameterContext.getParameter().getType().equals(DataBase.class);
    }

    @Override
    public Object resolveParameter(ParameterContext parameterContext, ExtensionContext extensionContext) 
      throws ParameterResolutionException {
        // The implementation... 
        // In this case, I'm retrieving the DataBase object from the SQL object 
        return SQL.getCurrentDataBase();
    }
}
```
````

--- 

<h1>JUnit Recap</h1>

<h4>So far we've covered the basics of JUnit and Unit testing!</h4>

<li>Installed all the prereq's</li>
<li>Ran a sample test and reviewed the results</li>
<li>Covered the basics: Display Name, Parameterized Tests, parameter sources, assertions</li>
<li>Ran a real test</li>
<li>Learned about more features: Lifecycle hooks and Extensions</li>

---

<h1>Resources</h1>
<div></div>
<a href="https://www.cypress.io/">Cypress</a>
<li>https://www.cypress.io/</li>
<a href="https://playwright.dev/">Playwright</a>
<li>https://playwright.dev/</li>
<a href="https://www.selenium.dev/">Selenium</a>
<li>https://www.selenium.dev/</li>
<a href="https://junit.org/junit5/">JUnit</a>
<li>https://junit.org/junit5/</li>
<a href="https://site.mockito.org/">Mockito</a>
<li>https://site.mockito.org/</li>
<a href="https://www.baeldung.com/java-profilers">Java Profilers</a>
<li>https://www.baeldung.com/java-profilers</li>
<a href="https://sli.dev/">This was built with Sli Dev!</a>
<li>https://sli.dev/</li>