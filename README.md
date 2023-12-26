# Activity 9 - Next Data Fetching UI Dev

**Deadline for Completion:** Friday, 29th December 2023 @ 11:59 PM GMT

## Overview
This project demonstrates basic data fetching from a REST API and displays the data in a user-friendly interface. It uses Next.js with TypeScript and incorporates Tailwind CSS with DaisyUI for styling. The data from three endpoints (`posts`, `users`, `albums`) is formatted into distinct UI elements - a paragraph, a table, and a 3-column grid card.

## Objective
To build a Next.js demo application that:
- Fetches data from specified API endpoints.
- Formats and displays the data in different UI components.
- Ensures code readability and maintainability.

## Testing Challenges

1. **Basic Understanding (30%)**: Evaluate how well the project structure and code organization reflect an understanding of Next.js and TypeScript fundamentals.
2. **TypeScript/JavaScript (15%)**: Assess the use of TypeScript features for type safety and effective use of JavaScript functions.
3. **UI/UX (15%)**: Analyze the design and usability of the UI elements in rendering the fetched data.
4. **Creativity/Innovation (10%)**: This involves the use of unique approaches to solve problems, the introduction of new ideas, and the ability to think outside the box.

## Directory Structure
```pwsh
activity9-[your-github-username]/
│
├──.next/
│
├── app/
│   ├── components/
│   │   │
│   │   ├── Posts/
│   │   │   ├── Posts.tsx
│   │   │   └── Posts.module.css
│   │   │
│   │   ├── Users/
│   │   │   ├── Users.tsx
│   │   │   └── Users.module.css
│   │   │
│   │   └── Albums/
│   │       ├── Albums.tsx
│   │       └── Albums.module.css
│   │
│   ├── globals.css
│   │
│   └── page.tsx
│
├── node_modules/ 
│
├── public/
│
├── tailwind.config.js
├── postcss.config.js
├── tsconfig.json
├── package.json
│
└── other files
```

## Boilerplate Code

### 1. Setting Up the Project
  - Create a project directory with the name `activity9-[your-github-username]`, replacing `[your-github-username]` with your actual GitHub username.

  - Launch your project in Visual Studio Code and synchronize it with the online repository. Ensure you have accepted the invitation to contribute to the repository, as this is a prerequisite for moving forward:
    ```pwsh
    git clone https://github.com/user/repo.git .
    ```

  - Install Next.js, Tailwind CSS, and DaisyUI:
    ```pwsh
    npx create-next-app@latest .
    npm install daisyui --save-dev
    ```

### 2. Configuring Tailwind CSS
Edit `tailwind.config.js` to include DaisyUI plugin:
```javascript
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx}",
    // other paths...
  ],
  theme: {
    extend: {},
  },
  plugins: [require('daisyui')],
}
```

### 3. Creating Components
For each endpoint, create a component and its corresponding CSS module. For example, `Posts.tsx` and `Posts.module.css` inside the `Posts` folder.

### 4. Fetching Data
In each component, use the `fetch` function to retrieve data from the respective endpoints. 

- Example for the `Posts` component:

  Posts.tsx
  ```typescript
  import React, { useState, useEffect, FC } from 'react';
  import styles from './Posts.module.css';

  interface Post {
    userId: number;
    id: number;
    title: string;
    body: string;
  }

  const Posts: FC = () => {
    const [posts, setPosts] = useState<Post[]>([]);

    useEffect(() => {
      fetch('https://jsonplaceholder.typicode.com/posts')
        .then(response => response.json())
        .then(data => setPosts(data as Post[]));
    }, []);

    return (
      <div>
        {posts.map(post => (
          <div key={post.id} className={styles.post}>
            <h3>{post.title}</h3>
            <p>{post.body}</p>
          </div>
        ))}
      </div>
    );
  };

  export default Posts;
  ```

  Posts.module.css
  ```css
  .post {
    /* Styling for individual posts */
  }
  ```
  
- Example for the `Users` component:

  Users.tsx
  ```typescript
  import React, { useState, useEffect, FC } from 'react';
  import styles from './Users.module.css';

  interface User {
    id: number;
    name: string;
    email: string;
    address: {
      city: string;
      // Include other relevant fields
    };
    // Other user fields
  }

  const Users: FC = () => {
    const [users, setUsers] = useState<User[]>([]);

    useEffect(() => {
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => setUsers(data as User[]));
    }, []);

    return (
      <div className={styles.tableContainer}>
        <table className={styles.table}>
          <thead>
            <tr>
              <th>Name</th>
              <th>Email</th>
              <th>City</th>
              {/* Other headings */}
            </tr>
          </thead>
          <tbody>
            {users.map(user => (
              <tr key={user.id}>
                <td>{user.name}</td>
                <td>{user.email}</td>
                <td>{user.address.city}</td>
                {/* Other data */}
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    );
  };

  export default Users;
  ```

  Users.module.css
  ```css
  .tableContainer {
    /* Styling for table container */
  }

  .table {
    /* Styling for table */
  }
  ```
  
- Example for the `Albums` component:

  Albums.tsx
  ```typescript
  import React, { useState, useEffect, FC } from 'react';
  import styles from './Albums.module.css';

  interface Album {
    userId: number;
    id: number;
    title: string;
  }

  const Albums: FC = () => {
    const [albums, setAlbums] = useState<Album[]>([]);

    useEffect(() => {
      fetch('https://jsonplaceholder.typicode.com/albums')
        .then(response => response.json())
        .then(data => setAlbums(data as Album[]));
    }, []);

    return (
      <div className={styles.gridContainer}>
        {albums.map(album => (
          <div key={album.id} className={styles.card}>
            <h3>{album.title}</h3>
          </div>
        ))}
      </div>
    );
  };

  export default Albums;
  ```

  Albums.module.css
  ```css
  .gridContainer {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    /* Additional styling */
  }

  .card {
    /* Styling for individual cards */
  }
  ```

### 5. Displaying Data
Use appropriate UI elements to display the data. Ensure that the UI is neither too simple nor too advanced, keeping in mind basic UI/UX principles.

### 6. Layout and Routing
Utilize the latest app router structure with the `/app` folder. Define the layout and include your components in `page.tsx`.
