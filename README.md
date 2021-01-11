# Reduce excercises
Examples for using common reduce functions.

## Using express middleware
Use multiple middlewares in an express app.

### Example input
```javascript
const application = express();
const middlewares = [
  helmet,
  compression,
  json,
  router,
  errorInterceptor
];
```

### Example output
```javascript
  application
```

### Example solution
<details>
  <summary>Click to expand!</summary>

```javascript
middlewares.reduce((app, middleware) => app.use(middleware), application);
```
</details>
