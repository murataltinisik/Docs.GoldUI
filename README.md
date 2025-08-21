# Gold UI Kit v2

**Gold UI Kit** is a modern, customizable, and themeable component library for React, built with **TypeScript** and **Tailwind CSS**.  
It provides a comprehensive set of accessible UI components designed to accelerate modern frontend development.

![npm](https://img.shields.io/npm/v/gold-ui-kit?color=gold&label=npm) 
![License](https://img.shields.io/npm/l/gold-ui-kit) 
![Minified](https://img.shields.io/bundlephobia/min/gold-ui-kit)

---

## 🚀 Get Started

GoldUI components are designed to be lightweight, flexible, and easy to integrate into any React project.  
After installing the package and configuring Tailwind CSS, you can start importing and using components directly.

- ✅ Use **named imports** to include only the components you need.  
- ⚡ Combine components to build complex UIs effortlessly.  
- 🎨 Customize via Tailwind classes or extend with your own styles.  

---

### 📄 Import Styles

```tsx
import "gold-ui-kit/dist/style.css";
// This line is required to apply GoldUI's default Tailwind-based styles.
// Without it, components may not appear styled correctly.
```

---

### 🛠 GoldUI Provider

`GoldUIProvider` is the root context provider for the GoldUI system.  
It enables global features like theming, responsive styling, and shared configuration across all components.

```tsx
<GoldUIProvider>
  <App />
</GoldUIProvider>
```

With custom theme:

```tsx
<GoldUIProvider theme={{ mode: "dark", colors: { primary: "green", danger: "orange" } }}>
  <App />
</GoldUIProvider>
```

---

### 🌗 Toggle Theme

The `toggleTheme` function in GoldUI allows you to dynamically switch between light and dark themes in your application.

- Updates the mode state in `GoldUIProvider`.  
- Applies or removes the `dark` class from `<html>` (TailwindCSS dark mode).  
- Saves the selected mode in **localStorage**, persisting across reloads.  

```tsx
const { mode, toggleTheme } = useTheme();

<button onClick={toggleTheme}>
  {mode === "dark" ? "Switch to Light Mode" : "Switch to Dark Mode"}
</button>
```

This allows you to add a dark mode toggle in your UI without writing any extra logic.

---

### 🔔 Toast Provider

`GoldToastProvider` enables global toast notification support.  
It allows you to use the `goldToast` utility (e.g., `goldToast.success("...")`) from anywhere in your app.

```tsx
<GoldUIProvider>
  {/* TOAST */}
  <GoldToastProvider />

  {/* APP */}
  <App />
</GoldUIProvider>
```

Usage:

```tsx
goldToast.success("Operation successful!", "solid");
```

---

## 📦 Installation

GoldUI v2 is a fully refactored, modern, and developer-first React component library built on Tailwind CSS.  
With a new theme system, improved accessibility, and performance-optimized components, GoldUI v2 empowers you to build dashboards, form-intensive apps, and design systems faster and more customizable than ever.

### Install via npm / yarn

```bash
npm install gold-ui-kit
# or
yarn add gold-ui-kit
```

---

### 🧩 Peer Dependencies

Make sure the following packages are already installed in your project:

```bash
npm install react react-dom
```

---

### ⚡ TailwindCSS Setup

To use GoldUI, your project must be configured with Tailwind CSS.  
If you're starting a new project with Vite, we recommend following the official Tailwind installation guide:

👉 [TailwindCSS with Vite](https://v3.tailwindcss.com/docs/guides/vite)

Make sure **tailwind.config.js** and **postcss.config.js** are correctly set up for smooth integration.

```js
// tailwind.config.js
module.exports = {
  darkMode: "class",
  content: ["./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

---

## 📄 License

MIT © [Gold UI](https://github.com/murataltinisik)
