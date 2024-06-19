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

<h1>What is Software Testing?</h1>

<h2>The process of evaluating and verifying that a software product or application does what it’s supposed to do. 
  <sup>1</sup>
</h2> 
<div></div>
<h1 v-click> Why should I test? </h1>
  <li v-click>To make sure what you've written does what it is supposed to do.</li>
  <li v-click>To make sure that what you've written doesn't break some other functionality.</li>
  <li v-click>To speed up the development processs.</li>

<span>1:<a href="https://www.ibm.com/topics/software-testing">https://www.ibm.com/topics/software-testing</a></span>

---

<h1>How should I test? AKA, what are my testing options...</h1>

<h3>Types of Tests</h3>
  <li>Unit Tests</li>
  <li>Integration Tests</li>
  <li> End to End Tests</li>
  <li> Component Tests</li>
  <li> Benchmarking Tests</li>


---

<h1>Testing Tools</h1>
<li>Cypress</li>
<li>Selenium</li>
<li>Playwright</li>
<li>Junit</li>
<li>TestNG</li>
<li>Java Profiler</li>
<li>Java Microbenchmarking Harness</li>

---

<h1>Cypress</h1>

<h2>Install Cypress</h2>

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

<h1>Cypress</h1>

<h2>Install Cypress cont'd</h2>

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

<h1>How does it work?</h1>

<h2>In a nutshell</h2>

<li>Built with JavaScript/Node</li>
<li>Runs directly in the browser</li>

<a href="https://www.cypress.io/how-it-works">More details here.</a>

---

<h1>todo.cy.js</h1>
<pre>
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
    // One of the more common arguments is
    // any valid chainer that comes from Chai or Chai-jQuery or Sinon-Chai.
    cy.get(".todo-list li").first().should("have.text", "Pay electric bill");
    cy.get(".todo-list li").last().should("have.text", "Walk the dog");
  });
```
````