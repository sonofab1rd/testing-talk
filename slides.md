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

# Software Testing

The best talk in the world about Software Testing!

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---



# What is Software Testing?

Software testing is the process of evaluating and verifying that a software product or application does what it’s supposed to do. [^1]

[^1]: https://www.ibm.com/topics/software-testing

---

# Why should I test?

- To make sure what you've written does what it is supposed to do.
- To make sure that what you've written doesn't break some other functionality.
- To speed up the development processs.

---

# How should I test? AKA, what are my testing options...

---

### Types of Tests

- Unit Tests
- Integration Tests
- End to End Tests
- Component Tests
- Benchmarking Tests

---

### Testing Tools

- Cypress
- Selenium
- Playwright
- Junit
- TestNG
- Java Profiler
- Java Microbenchmarking Harness

---

# Cypress

### Install Cypress

- create a cypress-talk folder
```bash {0|1}
mkdir cypress-talk
```

- initialize with npm

```bash {0|1}
npm init
```

- enter through all the prompts
- add cypress

```bash {0|1}
npm install cypress --save-dev
```

- open cypress

```bash {0|1}
npx cypress open
```

---

# Cypress

### Install Cypress cont'd

- click End To End testing config option
- review added files
- click to continue
- Chrome Selected by default
- click Start E2E testing in chrome
- click scaffold example specs
- click ok!
- under 1 - getting started
- click todo to run the todo test

---

# What just happened?

Cypress opened up a webpage with a todo list, started getting elements on the page and asserting things about them, and listed out the results to the left. 

# How does it work?

### In a nutshell
- Built with JavaScript/Node
- Runs directly in the browser

[More details here.](https://www.cypress.io/how-it-works)

---

# todo.cy.js

```js {all}{maxHeight:'400px', lines:true}
describe('example to-do app', () => {
  beforeEach(() => {
    cy.visit('https://example.cypress.io/todo')
  })

  it('displays two todo items by default', () => {
    cy.get('.todo-list li').should('have.length', 2)
    cy.get('.todo-list li').first().should('have.text', 'Pay electric bill')
    cy.get('.todo-list li').last().should('have.text', 'Walk the dog')
  })

  it('can add new todo items', () => {
    const newItem = 'Feed the cat'

    cy.get('[data-test=new-todo]').type(`${newItem}{enter}`)

    cy.get('.todo-list li')
      .should('have.length', 3)
      .last()
      .should('have.text', newItem)
  })

  it('can check off an item as completed', () => {
    cy.contains('Pay electric bill')
      .parent()
      .find('input[type=checkbox]')
      .check()

    cy.contains('Pay electric bill')
      .parents('li')
      .should('have.class', 'completed')
  })

  context('with a checked task', () => {
    beforeEach(() => {
      cy.contains('Pay electric bill')
        .parent()
        .find('input[type=checkbox]')
        .check()
    })

    it('can filter for uncompleted tasks', () => {
      cy.contains('Active').click()

      cy.get('.todo-list li')
        .should('have.length', 1)
        .first()
        .should('have.text', 'Walk the dog')

      cy.contains('Pay electric bill').should('not.exist')
    })

    it('can filter for completed tasks', () => {
      cy.contains('Completed').click()

      cy.get('.todo-list li')
        .should('have.length', 1)
        .first()
        .should('have.text', 'Pay electric bill')

      cy.contains('Walk the dog').should('not.exist')
    })

    it('can delete all completed tasks', () => {
      cy.contains('Clear completed').click()

      cy.get('.todo-list li')
        .should('have.length', 1)
        .should('not.have.text', 'Pay electric bill')

      cy.contains('Clear completed').should('not.exist')
    })
  })
})
```