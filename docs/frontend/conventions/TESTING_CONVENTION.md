# Testing Convention

## BDD (Behavior-Driven Development) - Given When Then

We use BDD syntax (Given-When-Then) to write tests in a human-readable format. This makes tests serve as living
documentation and helps to understand what the application does.

**Vitest BDD example:**

```typescript
describe('<Button />', () => {       // Given
  describe('when clicked', () => {   // When
    it('calls the handler', () => {  // Then
      const handleClick = vi.fn();
      render(<Button onClick={handleClick}>Click me</Button>);

      fireEvent.click(screen.getByText('Click me'));

      expect(handleClick).toHaveBeenCalledTimes(1);
    });
  });
});
```

**Gherkin BDD example:**

```gherkin
Given a user is on the login page
When they enter valid credentials
Then they should be redirected to the dashboard
```

- [BDD introduction](https://cucumber.io/docs/bdd/)
- [Given-When-Then format](https://martinfowler.com/bliki/GivenWhenThen.html)
