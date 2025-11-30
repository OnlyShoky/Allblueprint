# Micro Frontends

**Definition:** An architectural style where independently deliverable frontend applications are composed into a greater whole.

## Key Concepts
- **Independence:** Teams can choose their stack (React, Vue, Angular) and deploy independently.
- **Integration:**
  - **Build-time:** npm packages (Not recommended, coupling).
  - **Run-time:** IFrames, Web Components, Module Federation (Webpack 5).

## Module Federation (Webpack 5)
Allows a JavaScript application to dynamically load code from another application.

```javascript
// host/webpack.config.js
new ModuleFederationPlugin({
  name: 'host',
  remotes: {
    app1: 'app1@http://localhost:3001/remoteEntry.js',
  },
});

// host/App.js
const RemoteApp = React.lazy(() => import('app1/App'));
```

**Pros:**
- Scalable frontend development.
- Independent deployments.
- Incremental upgrades.

**Cons:**
- Payload size (duplicate dependencies).
- Complexity in shared state and styling.
