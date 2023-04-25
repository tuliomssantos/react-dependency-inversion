# Dependency Inversion in React

## What is Dependency Inversion?

Dependency inversion is a principle of object-oriented programming that states that high-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

## Dependency Inversion in Functional Programming

In functional programming, we don't have objects, so we don't have the same problem. However, we do have functions that depend on other functions. We can apply the same principle to functions.

### Example

Let's say we have a function that fetches a user from a database:

```js
const fetchUser = (id) => {
  // fetch user from database
  return user;
};
```

This function is dependent on the database. We can invert this dependency by passing the database as an argument:

```js
const fetchUser = (db, id) => {
  // fetch user from database
  return user;
};
```

Now, the function is no longer dependent on the database. It's dependent on the database being passed as an argument. This is a good thing because it makes the function more flexible. We can now pass in any database we want.

## Dependency Inversion in React

In React, we have components that depend on other components. We can apply the same principle to components.

### Example

```tsx
import React, { useState, useEffect } from 'react';

interface UserService {
  getUser(): Promise<User>;
}

interface User {
  name: string;
  email: string;
}

interface Props {
  userService: UserService;
}

const MyComponent: React.FC<Props> = ({ userService }) => {
  const [user, setUser] = useState<User | null>(null);

  useEffect(() => {
    const fetchUser = async () => {
      const user = await userService.getUser();
      setUser(user);
    };

    fetchUser();
  }, [userService]);

  return (
    <div>
      {user ? (
        <>
          <h2>{user.name}</h2>
          <p>{user.email}</p>
        </>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
};

export default MyComponent;
```

In this example, MyComponent is a function component that takes a userService prop of type UserService. The component uses useState and useEffect hooks to manage the state of the component and fetch the user data from the userService. By passing the userService as a prop, we are using dependency inversion to decouple the component from the implementation of the UserService.