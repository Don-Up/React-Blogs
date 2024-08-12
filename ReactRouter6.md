# ReactRouter6

> npm install react-router-dom@6

1. Hierarchical structure: Router→Routes→Route.

2. Router is used to enable routing functionality in applications

3. Routes are used to define the routing configuration of an application.

4. Route is used to declare a single route (React Router 6 automatically matches routes accurately.

   1. Property 1: `path`, which specifies the route path. It can be a static route or a dynamic route (e.g., /users/).
   2. Property 2：`element`，which specifies the route component.
   3. 404 Routes：`<Route path="*" element={<NotFound />} />`, which specifies the 404 page.
   4. Nesting Routes: A Route can nest other Routes inside.

5. Accept dynamic route parameters.

   1. Approach 1: Use props to get it.

      ```javascript
      const UserDetail: React.FC<RouteComponentProps<{ id: string }>> = (props) => {
          const userId = props.match.params.id;
          // other logic
      };
      ```

    2. Approach 2：Use the **useParams** hook.

       ```javascript
       const { id } = useParams<{ id: string }>();
       ```

6. Programmatic Navigation

- **Using the `useNavigate` hook**: React Router 6 provides the `useNavigate` hook, which is used to perform navigation in code.

  ```jsx
  const Component: React.FC = () => {
      const navigate = useNavigate();
  
      const handleClick = () => {
          navigate('/path');  // 编程式导航到 /path
      };
  
      return <button onClick={handleClick}>Go to Path</button>;
  };
  ```

- **Use the `navigate` function**: In React event handlers or other business logic, you can use the `navigate` function to perform navigation.

  ```jsx
  const navigate = useNavigate();
  
  function handleNavigation() {
      // Navigate to the specified path
      // The optional indicates represents replacing the current history records.
      navigate('/another-path', { replace: true });  
  }
  ```

