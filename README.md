# Gold UI Kit

![npm](https://img.shields.io/npm/v/gold-ui-kit?color=gold&label=npm)
![License](https://img.shields.io/npm/l/gold-ui-kit)
![Minified](https://img.shields.io/bundlephobia/min/gold-ui-kit)

**Gold UI Kit** is a modern, accessible, customizable, and themeable React component library built with **TypeScript**.

GoldUI provides a collection of reusable components, a centralized theme system, global toast notifications, alerts, and a composable API designed for modern React applications.

> **GoldUI v3** introduces a redesigned provider architecture, semantic color tokens, global notification APIs, and a cleaner developer experience.

---

## ✨ Features

- ⚛️ Built for React
- 🔷 TypeScript-first API
- 🎨 Centralized theme system
- 🌗 Light and dark mode
- 🧩 Composable UI components
- 🔔 Global toast notifications
- 🚨 Global alert API
- 🎯 Semantic color tokens
- ♿ Accessibility-focused components
- 🌳 Named imports
- ⚡ Tree-shaking friendly
- 🛠 Customizable component APIs
- 📦 Lightweight and reusable
- 🧱 Layout primitives
- 🧭 Navigation components

---

## 📦 Installation

Install Gold UI Kit using npm:

```bash
npm install gold-ui-kit
```

Or with Yarn:

```bash
yarn add gold-ui-kit
```

GoldUI requires React and React DOM:

```bash
npm install react react-dom
```

---

# 🚀 Get Started

GoldUI v3 is designed around a small number of global providers and composable components.

## 1. Wrap your application

Import the GoldUI stylesheet and the providers you need.

```tsx
import "gold-ui-kit/dist/style.css";

import {
  GoldUIProvider,
  GoldToastProvider,
  GoldAlertProvider,
} from "gold-ui-kit";

createRoot(document.getElementById("root")!).render(
  <GoldUIProvider>
    <GoldToastProvider />
    <GoldAlertProvider />

    <App />
  </GoldUIProvider>
);
```

### Provider responsibilities

| Provider | Responsibility |
| --- | --- |
| `GoldUIProvider` | Theme and global GoldUI configuration |
| `GoldToastProvider` | Global toast notification host |
| `GoldAlertProvider` | Global alert host |

Only mount the global providers your application needs.

---

## 2. Use a component

GoldUI components use named imports.

```tsx
import { Button, Input, Card } from "gold-ui-kit";

export default function App() {
  return (
    <Card title="Sign up">
      <Input placeholder="you@example.com" />

      <Button className="mt-3">
        Continue
      </Button>
    </Card>
  );
}
```

Components can be combined freely to build forms, dashboards, navigation, dialogs, application shells, and other interfaces.

---

## 3. Use global APIs

Once the appropriate provider is mounted, GoldUI global APIs can be used from anywhere in your application.

```tsx
import { goldToast } from "gold-ui-kit";

goldToast.success("Saved!");
```

No prop drilling or application-level notification state is required.

---

# 🎨 Config Provider

`GoldUIProvider` is the root provider for the GoldUI system.

It provides:

- Theme configuration
- Light and dark mode
- Semantic colors
- Shared GoldUI configuration
- Global provider context

A typical application should mount `GoldUIProvider` once near the root of the application.

## Basic setup

```tsx
import { GoldUIProvider } from "gold-ui-kit";

function App() {
  return (
    <GoldUIProvider>
      <YourApplication />
    </GoldUIProvider>
  );
}
```

## Custom theme

GoldUI supports configuring the application theme through the provider.

```tsx
<GoldUIProvider
  theme={{
    mode: "dark",
    colors: {
      primary: "yellow",
      danger: "orange",
    },
  }}
>
  <App />
</GoldUIProvider>
```

The theme can define the active mode and semantic colors used throughout the application.

---

# 🎨 Semantic Color Tokens

GoldUI uses semantic color tokens instead of requiring every component to define its own colors.

| Token | Purpose |
| --- | --- |
| `primary` | Primary actions and brand UI |
| `success` | Successful operations and positive states |
| `warning` | Warnings and cautionary states |
| `danger` | Errors and destructive actions |
| `default` | Neutral UI states |

These tokens are shared across GoldUI components and global APIs.

This makes it possible to change the visual language of an application from a centralized configuration.

---

# 🌗 Light & Dark Mode

GoldUI provides built-in theme mode support.

Use the `useTheme` hook to access the current mode and toggle it.

```tsx
import { useTheme } from "gold-ui-kit";

export function ThemeToggle() {
  const { mode, toggleTheme } = useTheme();

  return (
    <button onClick={toggleTheme}>
      {mode === "dark"
        ? "Switch to Light Mode"
        : "Switch to Dark Mode"}
    </button>
  );
}
```

The `mode` value represents the current theme:

```text
"light"
```

or:

```text
"dark"
```

Calling `toggleTheme()` switches between the available modes.

---

## Theme example

```tsx
import { GoldUIProvider } from "gold-ui-kit";

export default function Root() {
  return (
    <GoldUIProvider
      theme={{
        mode: "dark",
        colors: {
          primary: "yellow",
          danger: "orange",
        },
      }}
    >
      <App />
    </GoldUIProvider>
  );
}
```

---

# 🔔 Toast API

GoldUI v3 includes a global toast notification system.

The toast API allows notifications to be triggered imperatively without passing notification state through your component tree.

## Setup

Mount `GoldToastProvider` once in your application.

```tsx
import { GoldToastProvider } from "gold-ui-kit";

function Root() {
  return (
    <GoldUIProvider>
      <GoldToastProvider />

      <App />
    </GoldUIProvider>
  );
}
```

Then import the global toast API:

```tsx
import { goldToast } from "gold-ui-kit";
```

---

## Status helpers

GoldUI provides semantic helpers for common notification states.

```tsx
goldToast.success("Profile saved");
goldToast.error("Something went wrong");
goldToast.warning("Storage is almost full");
goldToast.info("A new version is available");
goldToast.primary("Welcome back");
goldToast.dark("Copied to clipboard");
```

Available statuses:

- `success`
- `error`
- `warning`
- `info`
- `primary`
- `dark`

---

# 🎨 Toast Variants

Toast calls can optionally specify a visual variant.

```tsx
goldToast.success("Deployed", "solid");

goldToast.warning("Heads up", "glass");
```

The documented variants include:

- `card`
- `solid`
- `outline`
- `glass`

---

# ⚙️ Toast Options

For more advanced notifications, pass an options object.

```tsx
goldToast.success("Order shipped", {
  title: "Order #824",
  description: "Your package will arrive in 2 days.",
  duration: 8000,
  action: {
    label: "View order",
    onClick: () => {
      // Open order
    },
  },
});
```

Common options:

| Option | Description |
| --- | --- |
| `title` | Notification title |
| `description` | Additional notification content |
| `duration` | How long the toast remains visible |
| `action` | Optional action displayed with the toast |

---

# 🛠 Toast Provider Options

The global toast provider can be configured once for the entire application.

```tsx
<GoldToastProvider
  placement="top-right"
  duration={4000}
  dismissible
  max={4}
/>
```

| Option | Description |
| --- | --- |
| `placement` | Position of the toast stack |
| `duration` | Default toast duration |
| `dismissible` | Allows users to dismiss notifications |
| `max` | Maximum number of visible notifications |

---

# 🚨 Alert API

GoldUI v3 also provides a global Alert API for application-level alerts, confirmations, and user decisions.

Mount the alert provider once:

```tsx
import { GoldAlertProvider } from "gold-ui-kit";

function Root() {
  return (
    <GoldUIProvider>
      <GoldToastProvider />
      <GoldAlertProvider />

      <App />
    </GoldUIProvider>
  );
}
```

The global alert API can then be imported from GoldUI:

```tsx
import { goldAlert } from "gold-ui-kit";
```

---

## Basic alert

```tsx
goldAlert.show("Profile saved");
```

---

## Confirmation flows

```tsx
const result = await goldAlert.confirm({
  title: "Delete account?",
  description: "This action cannot be undone.",
});

if (result) {
  // Continue with the action
}
```

The returned result can be used to determine whether the user confirmed the operation.

---

## Alert actions

```tsx
goldAlert.confirm({
  title: "Delete project?",
  description: "This action cannot be undone.",
  confirmText: "Delete",
  cancelText: "Cancel",
  onConfirm: () => {
    // Delete project
  },
});
```

Useful for:

- Delete confirmations
- Destructive operations
- Permission requests
- Important user decisions
- Application warnings

---

# 🧩 Components

GoldUI v3 organizes components into several categories.

## General

- `Button`
- `ButtonGroup`
- `ActionButton`
- `FloatButton`

## Layout

- `Box`
- `Flex`
- `Grid`
- `Divider`
- `Splitter`
- `Footer`

## Navigation

- `Tab`
- `Link`
- `Step`
- `Menu`
- `Dropdown`
- `Breadcrumb`
- `Pagination`
- `Toolbar`

More components are available in the v3 component catalog.

---

# 🌳 Named Imports

GoldUI uses named imports throughout the component library.

```tsx
import {
  Button,
  Input,
  Card,
  Box,
  Flex,
  Grid,
} from "gold-ui-kit";
```

This keeps imports explicit and works well with modern bundlers and tree-shaking.

---

# ♿ Accessibility

GoldUI is designed with accessible UI patterns in mind.

When building interfaces with GoldUI:

- Prefer semantic HTML where possible.
- Provide meaningful labels for form controls.
- Use buttons for actions and links for navigation.
- Provide accessible names for icon-only controls.
- Preserve keyboard accessibility.
- Avoid removing focus indicators without providing an alternative.
- Use the appropriate semantic component for the intended interaction.

GoldUI components provide accessible foundations while application-level content and usage still determine the final accessibility of an interface.

---

# 🧱 Composing Components

GoldUI components are designed to be composed rather than used as isolated widgets.

```tsx
import {
  Card,
  Flex,
  Input,
  Button,
} from "gold-ui-kit";

export function LoginForm() {
  return (
    <Card title="Sign in">
      <Flex className="flex-col gap-4">
        <Input
          placeholder="Email"
          type="email"
        />

        <Input
          placeholder="Password"
          type="password"
        />

        <Button>
          Sign in
        </Button>
      </Flex>
    </Card>
  );
}
```

---

# 🎯 Using Tailwind Classes

GoldUI components can be customized using classes where supported.

```tsx
<Button className="mt-4 w-full">
  Continue
</Button>
```

You can combine GoldUI components with your application's existing Tailwind utility classes.

GoldUI v3's provider and theme system should be used for global visual configuration, while component classes can be used for local layout and styling adjustments.

---

# 🏗 Recommended Application Structure

A typical GoldUI v3 application can be initialized like this:

```tsx
import "gold-ui-kit/dist/style.css";

import {
  GoldUIProvider,
  GoldToastProvider,
  GoldAlertProvider,
} from "gold-ui-kit";

import App from "./App";

createRoot(document.getElementById("root")!).render(
  <GoldUIProvider>
    <GoldToastProvider />
    <GoldAlertProvider />

    <App />
  </GoldUIProvider>
);
```

Your application components can then use GoldUI normally:

```tsx
import {
  Button,
  Card,
  Input,
  goldToast,
} from "gold-ui-kit";

export default function App() {
  const handleSave = () => {
    goldToast.success("Saved successfully");
  };

  return (
    <Card title="Example">
      <Input placeholder="Enter your name" />

      <Button onClick={handleSave}>
        Save
      </Button>
    </Card>
  );
}
```

---

# 📁 Suggested Project Structure

```text
src/
├── components/
│   ├── Header.tsx
│   ├── Sidebar.tsx
│   └── Dashboard.tsx
│
├── pages/
│   ├── Home.tsx
│   └── Settings.tsx
│
├── App.tsx
└── main.tsx
```

GoldUI acts as the UI foundation while application-specific components remain inside your own project.

---

# 🔄 Global APIs vs Components

GoldUI provides both declarative components and imperative global APIs.

### Components

Use components when UI belongs directly to your React tree:

```tsx
<Button>
  Save
</Button>
```

### Toast API

Use `goldToast` for temporary global notifications:

```tsx
goldToast.success("Saved!");
```

### Alert API

Use `goldAlert` for alerts and user decisions:

```tsx
await goldAlert.confirm({
  title: "Continue?",
  description: "Please confirm this action.",
});
```

### Theme API

Use `useTheme` for runtime theme interaction:

```tsx
const { mode, toggleTheme } = useTheme();
```

---

# 📚 API Overview

| API | Purpose |
| --- | --- |
| `GoldUIProvider` | Root GoldUI configuration and theme |
| `GoldToastProvider` | Toast notification host |
| `GoldAlertProvider` | Alert host |
| `useTheme` | Access and toggle theme mode |
| `goldToast` | Imperative toast notifications |
| `goldAlert` | Imperative alerts and confirmations |

---

# 📦 Package Exports

GoldUI is consumed from the main package:

```tsx
import {
  Button,
  Input,
  Card,
  GoldUIProvider,
  GoldToastProvider,
  GoldAlertProvider,
  useTheme,
  goldToast,
  goldAlert,
} from "gold-ui-kit";
```

Styles are imported separately:

```tsx
import "gold-ui-kit/dist/style.css";
```

The stylesheet should be loaded once by the application.

---

# 🔐 TypeScript

GoldUI is written with TypeScript and provides typed component APIs.

TypeScript users can take advantage of autocomplete and type checking throughout the GoldUI API.

---

# 🌓 Complete Setup Example

```tsx
import "gold-ui-kit/dist/style.css";

import {
  GoldUIProvider,
  GoldToastProvider,
  GoldAlertProvider,
  Button,
  Card,
  Input,
  useTheme,
  goldToast,
} from "gold-ui-kit";

function ThemeToggle() {
  const { mode, toggleTheme } = useTheme();

  return (
    <Button onClick={toggleTheme}>
      {mode === "dark"
        ? "Switch to Light Mode"
        : "Switch to Dark Mode"}
    </Button>
  );
}

function App() {
  const handleSave = () => {
    goldToast.success("Changes saved");
  };

  return (
    <Card title="GoldUI Example">
      <Input placeholder="you@example.com" />

      <div className="mt-4 flex gap-2">
        <Button onClick={handleSave}>
          Save
        </Button>

        <ThemeToggle />
      </div>
    </Card>
  );
}

createRoot(document.getElementById("root")!).render(
  <GoldUIProvider
    theme={{
      mode: "light",
      colors: {
        primary: "yellow",
        danger: "orange",
      },
    }}
  >
    <GoldToastProvider
      placement="top-right"
      duration={4000}
      dismissible
      max={4}
    />

    <GoldAlertProvider />

    <App />
  </GoldUIProvider>
);
```

---

# 🛠 Development

Clone the repository:

```bash
git clone https://github.com/murataltinisik/gold-ui-kit.git
```

Install dependencies:

```bash
npm install
```

Start the development environment:

```bash
npm run dev
```

Build the package:

```bash
npm run build
```

Run tests:

```bash
npm test
```

> Available development scripts may vary depending on the current package configuration.

---

# 🤝 Contributing

Contributions, issues, and feature requests are welcome.

Before submitting a pull request:

1. Create a branch for your change.
2. Keep changes focused.
3. Follow the existing TypeScript and React conventions.
4. Add or update tests where appropriate.
5. Update documentation for public API changes.
6. Verify the package builds successfully.

---

# 📖 Documentation

Full GoldUI v3 documentation:

https://v3.goldui.com/

The documentation includes:

- Installation
- Get Started
- Config Provider
- Theming
- Toast API
- Alert API
- Components
- Component categories
- API examples

---

# 📄 License

MIT © Gold UI