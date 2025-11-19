# Testing

## Approach

We follow a **test pyramid** strategy: many unit tests and minimal
end-to-end tests. This approach ensures fast feedback loops while maintaining confidence in our code quality.

## Unit Testing

**Tools**: Vitest + React Test Renderer + @testing-library/react

**Target Coverage**: 95-100%

Unit tests are the foundation of our testing strategy. They run quickly and provide immediate feedback during development.
We aim for high coverage to ensure that individual components and functions work correctly in isolation.

- [Vitest documentation](https://vitest.dev/)
- [Testing Library documentation](https://testing-library.com/)
- [React Testing Library best practices](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)

## End-to-End Testing

**Tools**: Playwright + Gherkin

**Target Coverage**: All happy paths

E2E tests validate complete user workflows and ensure that the application works correctly from the user's perspective.
We focus on testing critical happy paths rather than exhaustive edge cases, which are better covered by unit tests.

- [Playwright documentation](https://playwright.dev/)
- [Gherkin syntax guide](https://cucumber.io/docs/gherkin/)

## Resources

- [Testing Convention](../conventions/TESTING_CONVENTION.md)