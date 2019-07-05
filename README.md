# Testing React

* [Frontend Masters - Testing React Applications v2](https://frontendmasters.com/courses/testing-react/)
* [github (fem-2018 branch + my solutions)](https://github.com/mjlyons/testing-workshop/tree/mjlyons/class-complete)

## Jest

### Jest Commands

jest —coverage
jest —watch

### Jest lint

`eslint-plugin-jest`

- `no-large-snapshots`: set a limit for snapshot size to not cram too much into a single test

### Mocking

[ ] https://blog.kentcdodds.com/but-really-what-is-a-javascript-mock-10d060966f7d
- `jest.mock(importpath, mockedThing)`
- simulate time passing: jest.userFakeTimers(), jest.runAllTimers()

### Expect commands:

* [expect() docs](https://facebook.github.io/jest/docs/en/expect.html)
* expect(element.textContent).toMatch(/.../) - regex on text without tags
* validate dates: `expect.toBeGreaterThanOrEqual()`, `expect.toBeLessThanOrEqual()`

### matching

* allow anything that's a string (rather than a particular string): `expect.any(String)`

### Jest.config.js

* “\\.module\\.css”: ‘identity-obj-proxy’
    * Accessing a property returns the name of that property
* “\\.css”: require.resolve($MODULE_PATH)
    * Mock an import
    * Could use for graphql
* `setupTestFrameworkScriptFile`: `require.resolve($MODULE_PATH)`
	- Run before tests
* `collectCoverageFrom`: whitelist of files to check coverage
* `coverageThreshold`: test fails if total coverage drops below X% (use 2% points lower than current avgs)
* `modulePaths`: configure what can be imported by name (rather than relative paths)

## Snapshots

[ ] [Blogpost: Effective snapshot testing](https://kentcdodds.com/blog/effective-snapshot-testing/)
- jest.config.js: `snapshotSerializers`: define alternate snapshot serialization logic
	- `jest-glamor-react`: serialize CSS-in-JS (if using Glamor)

## react-testing-library

- [github](https://github.com/testing-library/react-testing-library)
- `wait`: async fn that resolves once cb does not throw error (similar to selenium's `await()`)
- `renderWithRouter()`: specify URL for integration tests
- `createMemoryHistory()`: mock browser history 
- `getByText()` finds element by text content
- `getByLabelText()` finds element by corresponding label text content
- `getByTestId()`: finds element matching attr `data-testid`
- render vs renderIntoDocument: whether want to trigger document-generated events
  - submitButton.click -> triggers submit event
  - node.click() triggers click (not DOM-initiated)
- afterEach(cleanup): removes component from DOM (including container), unmount removes component from DOM but not container

## Cypress

- to run: `npx cypress open`
- config file: `cypress.json`
- `cypress-testing-library` (like react-testing-library -- getByText(), etc.)
- "command": a tracked "step" in the test
- js devtools console shows command/visited-node
- cleanup at start of test in case you need to debug test at end
- `npm-run-all --parallel`: runs multiple npm scripts in parallel (useful for running server & cypress concurrently)
- `npm-run-all --parallel -race`: kills all scripts once any exists (useful for CI)
- `cypress open`: Opens browser to run cypress tests (useful for Dev)
- `cypress run`: Runs cypress headless (CI)
- **cypress only supports Chrome (and electron?)**
