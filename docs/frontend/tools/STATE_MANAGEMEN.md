## State Management

### Primary Strategy: React Context + useState

For most state management needs, we use React's built-in `useContext` and `useState` hooks. This approach is simple, requires no additional dependencies, and is sufficient for most applications.

We prefer this for:

- Global application state (theme, user preferences)
- Shared state between closely related components
- Simple state that doesn't require complex logic

### Secondary Strategy: Zustand

When state management becomes more complex or we need better performance for frequently updated state, we use Zustand. Zustand is a lightweight state management solution that provides:

- Minimal boilerplate
- Better performance than Context for frequently updated state
- Simple API that's easy to learn and use
- TypeScript support out of the box

We use Zustand for:

- Complex global state with multiple actions
- State that needs to persist across sessions
- State that requires middleware (logging, persistence, etc.)

### Resources

- [Zustand documentation](https://zustand-demo.pmnd.rs/)
- [Zustand GitHub repository](https://github.com/pmndrs/zustand)
- [React Context API documentation](https://react.dev/reference/react/useContext)
