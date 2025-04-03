# React Frontend for Spring Boot Monolithic Application

## Table of Contents
- [Introduction](#introduction)
- [Project Setup](#project-setup)
  - [Installing Vite](#installing-vite)
  - [Installing Dependencies](#installing-dependencies)
  - [Setting up Tailwind CSS](#setting-up-tailwind-css)
- [Dependency Overview](#dependency-overview)
  - [React Redux & Redux Toolkit](#react-redux--redux-toolkit)
  - [React Spinner](#react-spinner)
  - [React Swiper](#react-swiper)
  - [Axios](#axios)
  - [React Hook Form](#react-hook-form)
  - [React Router DOM](#react-router-dom)
  - [React Hot Toast](#react-hot-toast)
  - [React Icons](#react-icons)
  - [Headless UI](#headless-ui)
  - [Material UI](#material-ui)
- [Integration with Spring Boot](#integration-with-spring-boot)
- [Running the Application](#running-the-application)
- [Contributing](#contributing)
- [License](#license)

---

## Introduction
This project serves as the frontend for a **Spring Boot Monolithic Application**. It is built using **React** with **Vite** for performance optimization. The project integrates Redux for state management, TailwindCSS for styling, and several UI/UX-enhancing libraries.

## Project Setup

### Installing Vite
To create a new React project using Vite, run:

```sh
npm create vite@latest my-react-app --template react
cd my-react-app
npm install
```

### Installing Dependencies
After setting up Vite, install the required dependencies:

```sh
npm install react-redux @reduxjs/toolkit react-spinners swiper axios react-hook-form react-router-dom react-hot-toast react-icons @headlessui/react @mui/material @mui/icons-material
```

### Setting up Tailwind CSS
Install Tailwind CSS, PostCSS, and autoprefixer:

```sh
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Configure `tailwind.config.js`:

```js
module.exports = {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: { extend: {} },
  plugins: [],
};
```

Add Tailwind to `src/index.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Dependency Overview

### React Redux & Redux Toolkit
Used for state management in large-scale applications.

### React Spinner
Provides loading indicators for better UX.

### React Swiper
Adds carousel functionality for displaying content in sliders.

### Axios
Handles HTTP requests and integrates seamlessly with Spring Boot APIs.

### React Hook Form
Simplifies form handling with built-in validation.

### React Router DOM
Enables navigation between pages in a React single-page application.

### React Hot Toast
Provides lightweight toast notifications.

### React Icons
Integrates popular icon sets for UI enhancement.

### Headless UI
Provides unstyled UI components, giving full customization control.

### Material UI
A robust UI component library for building professional-looking interfaces.

## Integration with Spring Boot

- Ensure the **Spring Boot backend** runs on a different port (e.g., `http://localhost:8080`).
- Configure `proxy` in `vite.config.js` to handle API calls:

```js
export default defineConfig({
  server: {
    proxy: {
      '/api': 'http://localhost:8080'
    }
  }
});
```

- Use Axios to connect React with Spring Boot:

```js
import axios from 'axios';

const API = axios.create({ baseURL: '/api' });

export default API;
```

## Running the Application

Start the development server:

```sh
npm run dev
```

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)
