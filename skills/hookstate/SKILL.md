---
name: hookstate
description: Guide for using Hookstate state management library. Use when implementing state management with Hookstate in React applications, setting up global/local states, or working with nested state structures.
---

# Hookstate State Management

Hookstate is a fast, flexible state management library based on React state hook with support for global, local, nested, and scoped states.

## Installation

```bash
npm install --save @hookstate/core
# or
yarn add @hookstate/core
```

## Core Concepts

- **Global states**: Created with `hookstate()`, persist across application lifecycle
- **Local states**: Created with `useHookstate()`, tied to component mount/unmount
- **Nested state**: Drill down to nested properties, all are State objects with same API
- **Scoped state**: Share state between components without performance penalty
- **Extensions**: Add plugins for persistence, validation, devtools, etc.

## Basic Usage

### Local State (Component-scoped)

```typescript
import { useHookstate } from '@hookstate/core'

function Counter() {
  const state = useHookstate(0) // or useHookstate({ count: 0 })
  
  return (
    <div>
      <p>Count: {state.value}</p>
      <button onClick={() => state.set(p => p + 1)}>Increment</button>
    </div>
  )
}
```

### Global State (Application-scoped)

```typescript
import { hookstate } from '@hookstate/core'

// Create global state outside component
const globalState = hookstate({
  user: null,
  theme: 'dark'
})

function UserProfile() {
  const state = useHookstate(globalState)
  
  return <p>User: {state.user.value}</p>
}
```

## State Updates

### Set (Replace entire state)

```typescript
state.set(newValue)
state.set(prev => prev + 1) // functional update
```

### Merge (Partial update)

```typescript
state.merge({ theme: 'light' }) // merges with existing
state.nested.prop.set('new value') // update nested property
```

### Nested State Updates

```typescript
const state = useHookstate({
  user: {
    name: 'John',
    address: {
      city: 'NYC'
    }
  }
})

// Drill down to nested properties
state.user.name.set('Jane')
state.user.address.city.set('LA')

// All nested levels are State objects with same API
```

## Best Practices

### Use Objects for Complex State

```typescript
// Good
const state = useHookstate({
  items: [],
  loading: false,
  error: null
})

// Avoid Maps, use plain objects/Records
```

### Mutate Only via Hookstate Methods

```typescript
// Correct
state.set(newValue)
state.merge({ key: value })
state.nested.prop.set(value)

// Incorrect - direct mutation won't trigger re-renders
state.value.key = value
```

### Use TypeScript for Type Safety

```typescript
interface AppState {
  user: { name: string; email: string } | null
  theme: 'light' | 'dark'
}

const state = hookstate<AppState>({
  user: null,
  theme: 'dark'
})

// Full IntelliSense support
state.user?.name.set('John')
```

### State as Component Props

```typescript
// State can be passed as props, making them "writable"
function Child({ state }: { state: State<string> }) {
  return <input value={state.value} onChange={e => state.set(e.target.value)} />
}
```

### Scoped State for Shared State

```typescript
// Uplift state to parent when multiple children need it
// No performance penalty due to scoped state tracking
function Parent() {
  const formState = useHookstate({ name: '', email: '' })
  
  return (
    <>
      <NameField state={formState.name} />
      <EmailField state={formState.email} />
    </>
  )
}
```

## Common Patterns

### Loading/Error Pattern

```typescript
const state = useHookstate({
  data: null as Data | null,
  loading: false,
  error: null as Error | null
})

async function fetchData() {
  state.loading.set(true)
  state.error.set(null)
  try {
    const response = await api.getData()
    state.data.set(response)
  } catch (err) {
    state.error.set(err)
  } finally {
    state.loading.set(false)
  }
}
```

### Array Operations

```typescript
const state = useHookstate([{ id: 1, name: 'Item 1' }])

// Add item (recommended)
state[state.length].set({ id: 2, name: 'Item 2' })
// or
state.merge([{ id: 2, name: 'Item 2' }])

// Update item (recommended - only rerenders affected components)
state[0].name.set('Updated')

// Remove item (recommended)
import { none } from '@hookstate/core'
state[0].set(none)
// or
state.merge({ 0: none })

// Concat arrays
state.merge([{ id: 3, name: 'Item 3' }, { id: 4, name: 'Item 4' }])

// Partial updates (update index 0, delete index 1, add index 3)
state.merge({ 0: { id: 1, name: 'Updated' }, 1: none, 3: { id: 4, name: 'New' } })
```

### State in Dependency Lists

```typescript
// Hookstate uniquely supports mutable state in dependency lists
// No need to use .value or extract specific properties

useEffect(() => {
  // Automatically tracks which state segments are used
  console.log('User changed:', state.user.value)
}, [state]) // Only re-runs when state.user changes
```

## Extensions/Plugins

### DevTools

```bash
npm install --save @hookstate/devtools
```

```typescript
import { devtools } from '@hookstate/devtools'

const state = hookstate({ ... }, devtools({ key: 'my-app' }))
```

### Local Storage Persistence

```bash
npm install --save @hookstate/localstored
```

```typescript
import { localstored } from '@hookstate/localstored'

const state = hookstate(
  { theme: 'dark' },
  localstored({ key: 'user-preferences' })
)
```

### Validation

```bash
npm install --save @hookstate/validated
```

```typescript
import { validated } from '@hookstate/validated'

const state = hookstate(
  { email: '' },
  validated({
    email: (value) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)
  })
)
```

## Performance Tips

- Use scoped state to minimize re-renders
- Drill down to specific nested properties instead of accessing entire state
- Hookstate automatically tracks which state segments are used/updated
- Ideal for huge states and frequent updates due to unique tracking mechanism

## Important Notes

- Don't use Maps or cyclic references in state
- Always mutate via Hookstate methods (set, merge)
- States can be passed as props to make them writable
- Local states are destroyed on unmount, global states persist
- TypeScript provides full type inference for any complexity
