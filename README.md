# React Strapi-Style Submenu Navigation

## 📝 Description

This project implements a responsive navigation system inspired by Strapi's UI, built with React. It features a main navbar, a hero section, a toggleable sidebar for smaller screens, and dynamic submenus that appear when hovering over navigation links in the main navbar. The application utilizes the React Context API for global state management, handling the sidebar's open/closed state and tracking the currently active page link to display the corresponding submenu. The menu structure and content are driven by a centralized data file (`data.jsx`), making it easy to customize navigation links and submenu items.

## ✨ Features

- **Strapi-Inspired UI:** Mimics the look and feel of Strapi's navigation menus.
- **Responsive Design:**
  - Displays a full navbar with hoverable submenus on larger screens.
  - Shows a toggle button to open/close a sidebar navigation on smaller screens.
- **Dynamic Submenus:** Submenus appear smoothly as the user hovers over the main navigation links, displaying relevant sub-links.
- **Context API for State Management:** Uses React Context (`createContext`, `useContext`) and a custom hook (`useGlobalContext`) to manage the sidebar visibility (`isSidebarOpen`) and the active page for the submenu (`pageId`).
- **Data-Driven Menus:** Navigation links, submenus, and associated icons are defined in a separate `data.jsx` file for easy configuration.
- **Icon Integration:** Leverages `react-icons` for visual elements within the navigation and submenus.
- **Hover Intent Logic:** Includes logic (`onMouseLeave` in `Submenu`, `onMouseOver` in `Navbar`) to correctly handle showing and hiding the submenu based on mouse position.

## 🚀 Live Demo

[Link to Live Demo]()

## 🛠️ Technologies Used

- **Frontend:** React.js (Hooks: `useState`, `useContext`, `useRef`)
- **State Management:** React Context API
- **Icons:** `react-icons`
- **Unique IDs:** `nanoid` (used in `data.jsx`)
- **Styling:** CSS (including potential use of CSS variables, transitions, grid layout for submenus)
- **JavaScript:** Event Handling (`onMouseOver`, `onMouseEnter`, `onMouseLeave`), `Element.getBoundingClientRect()`

## ⚙️ Setup and Installation

To run this project locally, follow these steps:

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/NoToRacism/Strapi_Interface
    cd <your-repository-directory>
    ```

2.  **Install dependencies:**
    Make sure you have Node.js and npm (or yarn) installed.

    ```bash
    npm install
    # or
    yarn install
    ```

3.  **Run the development server:**
    ```bash
    npm start
    # or
    yarn start
    ```
    This will typically open the application in your default browser at `http://localhost:3000`.

## 📖 Usage / Integration

1.  **Wrap your App:** Ensure your main application component is wrapped with the `AppProvider` from `Context.jsx` to enable global state access.

    ```javascript
    // In main.jsx or index.js
    import React from "react";
    import ReactDOM from "react-dom/client";
    import App from "./App";
    import { AppProvider } from "./Context"; // Import the provider
    import "./index.css"; // Import CSS

    ReactDOM.createRoot(document.getElementById("root")).render(
      <React.StrictMode>
        <AppProvider>
          {" "}
          {/* Wrap App */}
          <App />
        </AppProvider>
      </React.StrictMode>
    );
    ```

2.  **Component Structure:** The `App` component renders `Navbar`, `Hero`, `Sidebar`, and `Submenu`.
3.  **Navbar Interaction:**
    - The `Navbar` contains `NavLinks` and a toggle button for the `Sidebar`.
    - Hovering over `NavLinks` triggers `setPageId` in the global context via `onMouseEnter`.
    - The `Navbar`'s `onMouseOver` helps reset `pageId` when the mouse isn't over a specific link, hiding the submenu.
4.  **Submenu Display:** The `Submenu` component listens for changes to `pageId` in the global context. When `pageId` is set, it finds the corresponding data in `sublinks` and renders the appropriate submenu content. It uses `onMouseLeave` and `getBoundingClientRect` logic to determine if the mouse has truly left the submenu area before hiding it.
5.  **Sidebar Toggle:** The `Sidebar` component's visibility is controlled by the `isSidebarOpen` state in the global context, toggled by functions (`openSidebar`, `closeSidebar`) accessed via the `useGlobalContext` hook.
6.  **Customization:** Modify `data.jsx` to change the navigation structure, links, icons, and submenu content. Adjust CSS files for styling.

## 🏗️ Project Structure

- `src/`: Contains the main source code.
  - `App.jsx`: Main application component, renders the layout components.
  - `Context.jsx`: Defines `AppContext`, `AppProvider` (holding `isSidebarOpen`, `pageId` state and related functions), and the `useGlobalContext` hook.
  - `Navbar.jsx`: Top navigation bar, includes logo, sidebar toggle button, and `NavLinks`. Handles mouse events to hide submenu when not hovering over links.
  - `NavLinks.jsx`: Renders the main navigation links based on `sublinks` data. Triggers `setPageId` on hover.
  - `Hero.jsx`: The main hero section component below the navbar.
  - `Sidebar.jsx`: Off-canvas menu for smaller screens, displays nested links from `sublinks`. Visibility controlled by context.
  - `Submenu.jsx`: Displays the dropdown/pop-up submenu based on the `pageId` from context. Contains logic to remain open while hovered.
  - `data.jsx`: Exports the `sublinks` array defining the structure and content of the navigation and submenus, utilizing `react-icons` and `nanoid`.
  - CSS Files (`index.css`, `App.css`, etc.): (Assumed) Contain styles for all components, including layout, responsiveness, and transitions.
- `public/`: Contains static assets.
- `package.json`: Lists project dependencies and scripts.

## 🤝 Contributing

Contributions are welcome! If you'd like to contribute, please follow these steps:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/your-feature-name`).
3.  Make your changes.
4.  Commit your changes (`git commit -m 'Add some feature'`).
5.  Push to the branch (`git push origin feature/your-feature-name`).
6.  Open a Pull Request.
