# Micro Frontends

#micro-frontends #frontend #architecture #modularity #trends

> [!important] Frontend Modularity
> Micro frontends extend microservices principles to the frontend—independent teams building and deploying frontend features autonomously.

**Related:** [[../ModernArchitectures/Monolith_Microservices|Microservices]] · [[../DesignPatterns/Architectural|Architectural Patterns]] · [[../BestPractices/CICD_DevOps|CI/CD]]

---

## Core Concept

**Definition:** An architectural style where independently deliverable frontend applications are composed into a greater whole.

**Goal:** Enable multiple teams to work on a large frontend application independently.

> [!success] Team Autonomy
> Each team owns a business capability end-to-end: backend APIs, database, AND frontend UI.

---

## Key Benefits

- **Independence:** Teams can choose their stack (React, Vue, Angular) and deploy independently
- **Faster Development:** Teams don't block each other
- **Incremental Upgrades:** Migrate to new frameworks gradually
- **Clear Ownership:** Each feature has a clear owner

---

## Integration Strategies

### 1. Build-Time Integration (Not Recommended)

**How:** Publish micro frontends as npm packages, import at build time.

> [!warning] Tight Coupling
> Build-time integration defeats the purpose of micro frontends. All apps must rebuild and redeploy together.

---

### 2. iFrames

**How:** Each micro frontend runs in an iframe.

**Pros:** Complete isolation, different  tech stacks  
**Cons:** Poor UX (routing, performance), styling challenges

> [!note] Simple But Limited
> iFrames work for simple cases but struggle with complex interactions.

---

### 3. Web Components

**How:** Each micro frontend is a custom element.

```javascript
// Define web component
class UserProfile extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<div>User Profile Widget</div>`;
  }
}
customElements.define('user-profile', UserProfile);

// Use in any framework
<user-profile user-id="123"></user-profile>
```

**Pros:** Framework-agnostic, native browser support  
**Cons:** Limited ecosystem, Shadow DOM complexity

---

### 4. Module Federation (Webpack 5) ⭐

**How:** Dynamically load code from other applications at runtime.

> [!success] Recommended Approach
> Module Federation provides the best balance of independence and integration.

**Example:**
```javascript
// app1/webpack.config.js (Host)
new ModuleFederationPlugin({
  name: 'host',
  remotes: {
    app1: 'app1@http://localhost:3001/remoteEntry.js',
    app2: 'app2@http://localhost:3002/remoteEntry.js',
  },
});

// app2/webpack.config.js (Remote)
new ModuleFederationPlugin({
  name: 'app2',
  filename: 'remoteEntry.js',
  exposes: {
    './Button': './src/Button',
    './Header': './src/Header',
  },
});

// host/App.js
const RemoteButton = React.lazy(() => import('app2/Button'));

function App() {
  return (
    <Suspense fallback="Loading...">
      <RemoteButton />
    </Suspense>
  );
}
```

**Related:** Enables [[../ModernArchitectures/Monolith_Microservices|microservices-style frontend]].

---

## Architecture Patterns

### Horizontal Split (by Page)

Each team owns complete pages/routes.

```
/products    → Products Team
/cart        → Cart Team
/checkout    → Checkout Team
```

**Pros:** Clear boundaries  
**Cons:** Inconsistent UX across pages

---

### Vertical Split (by Component)

Each team owns components on the same page.

```
Product Page:
  - Header        → Platform Team
  - Product Info  → Products Team
  - Recommendations → Recommendations Team
  - Reviews       → Reviews Team
```

**Pros:** Richer team ownership  
**Cons:** More complex integration

---

## Challenges

> [!warning] Complexity Trade-offs
> Micro frontends introduce operational complexity. Only adopt if you have the team scale to justify it.

| Challenge | Solution |
|-----------|----------|
| **Payload Size** | Share dependencies, lazy load |
| **Styling Conflicts** | CSS-in-JS, CSS Modules, Shadow DOM |
| **Shared State** | Event bus, URL state, shared context |
| **Routing** | Centralized router or meta-framework |
| **Performance** | Code splitting, CDN, preloading |

---

## When to Use

> [!question] Should You Use Micro Frontends?
> 
> **Use If:**
> - Multiple large teams (10+ developers each)
> - Different release cadences needed
> - Legacy migration (incremental rewrite)
> - Clear business domain boundaries
> 
> **Don't Use If:

**
> - Small team (< 10 developers)
> - Monolithic backend
> - Tight frontend coupling required

---

## Further Reading

- Apply [[../ModernArchitectures/Monolith_Microservices|microservices principles]]
- Deploy with [[../BestPractices/CICD_DevOps|independent CI/CD]]
- Monitor [[../BestPractices/Observability|frontend observability]]
- Test with [[../BestPractices/Testing_TDD_BDD|E2E tests]]

**Tags:** #micro-frontends #frontend #modularity #module-federation #architecture
