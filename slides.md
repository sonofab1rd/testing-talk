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

<div>The process of evaluating and verifying that a software product or application does what it’s supposed to do. 
  <sup>1</sup>
</div> 

<h3 v-click> Why should I test? </h3>
  <li v-click>To make sure what you've written does what you intended.</li>
  <li v-click>To make sure you haven't broken some other functionality.</li>
  <li v-click>To speed up the development processs.</li>

<h3 v-click>What are some common types?</h3>
  <li v-click>Unit Tests</li>
  <li v-click>Integration Tests</li>
  <li v-click> End to End Tests</li>
  <li v-click> Component Tests</li>
  <li v-click> Benchmarking Tests</li>

<span>1:<a href="https://www.ibm.com/topics/software-testing">https://www.ibm.com/topics/software-testing</a></span>

---

<h1>What are some testing tools?</h1>
<li>Cypress</li>
<li>Playwright</li>
<li>Selenium</li>
<li>Junit</li>
<li>Mockito</li>
<li>Java Profiler</li>

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

<h3>How does it work?</h3>

<h4>In a nutshell...</h4>

<li>Built with JavaScript/Node</li>
<li>Runs directly in the browser</li>
<li>Able to interact directly with the page</li>
<li>Different from Selenium. Which, must send requests to the page.</li>

<a href="https://www.cypress.io/how-it-works">More details here.</a>

---

<h1>todo.cy.js</h1>

<span>Path to todo.cy</span>

<pre class="text-size-xs ml-8">
cypress-talk
  cypress
  e2e
    1-getting-started
      todo.cy.js
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
layout: iframe

# the web page source
url: https://docs.cypress.io/guides/references/assertions

---

---
layout: iframe

# the web page source
url: https://jestjs.io/

---

---

<h1>A (more) real Cypress example</h1>

<a href="https://gitlab.openpracticesolutions.com/openpm/testing/cypress-openpm">cypress-openpm</a>

04_C215_Login_No_2_Factor.cy.js

cypress-openpm/cypress/e2e/Test/OpenPM/01_Login_Screen/04_C215_Login_No_2_Factor.cy.js

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