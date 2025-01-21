# PRACTICAL - 4
Sure, let's go through the steps to create a simple React application that demonstrates the use of React Context for managing shared state across multiple components.

### Step 1: Set up the React application

First, create a new React application using Create React App:

```bash
npx create-react-app counter-app
cd counter-app
```

### Step 2: Create the CounterContext

Create a new file `CounterContext.js` in the `src` directory:

```javascript
// src/CounterContext.js
import React, { createContext, useState } from 'react';

const CounterContext = createContext();

const CounterProvider = ({ children }) => {
    const [count, setCount] = useState(0);

    const increment = () => setCount(count + 1);
    const decrement = () => setCount(count - 1);

    return (
        <CounterContext.Provider value={{ count, increment, decrement }}>
            {children}
        </CounterContext.Provider>
    );
};

export { CounterContext, CounterProvider };
```

### Step 3: Wrap your app with the CounterProvider

Modify the `App.js` file to wrap the entire app with the `CounterProvider`:

```javascript
// src/App.js
import React from 'react';
import { CounterProvider } from './CounterContext';
import CounterDisplay from './CounterDisplay';
import CounterControls from './CounterControls';

function App() {
    return (
        <CounterProvider>
            <div className="App">
                <CounterDisplay />
                <CounterControls />
            </div>
        </CounterProvider>
    );
}

export default App;
```

### Step 4: Implement the CounterDisplay component

Create a new file `CounterDisplay.js` in the `src` directory:

```javascript
// src/CounterDisplay.js
import React, { useContext } from 'react';
import { CounterContext } from './CounterContext';

const CounterDisplay = () => {
    const { count } = useContext(CounterContext);

    return (
        <div>
            <h1>Counter: {count}</h1>
        </div>
    );
};

export default CounterDisplay;
```

### Step 5: Implement the CounterControls component

Create a new file `CounterControls.js` in the `src` directory:

```javascript
// src/CounterControls.js
import React, { useContext } from 'react';
import { CounterContext } from './CounterContext';

const CounterControls = () => {
    const { increment, decrement } = useContext(CounterContext);

    return (
        <div>
            <button onClick={increment}>Increment</button>
            <button onClick={decrement}>Decrement</button>
        </div>
    );
};

export default CounterControls;
```

### Step 6: Run the application

Now, you can run the application:

```bash
npm start
```

You should see a simple counter application where the current count is displayed in one component (`CounterDisplay`) and can be incremented or decremented using buttons in another component (`CounterControls`).

This setup demonstrates how to use React Context to manage shared state across multiple components without prop drilling.

Similar code found with 1 license type
