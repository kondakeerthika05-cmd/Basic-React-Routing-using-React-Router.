# Basic-React-Routing-using-React-Router.
1️⃣ Project Setup

Create a Vite + React app (if not already created):

npm create vite@latest react-routing-app
cd react-routing-app
npm install
npm install react-router-dom
npm run dev

2️⃣ Folder Structure (Important)
src/
│── components/
│   ├── Navbar.jsx
│   └── TodoCard.jsx
│
│── pages/
│   ├── Home.jsx
│   ├── AboutUs.jsx
│   ├── Todos.jsx
│   └── NotFound.jsx
│
│── App.jsx
│── main.jsx
│── index.css

3️⃣ Routing Setup (main.jsx)
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);


✔ Uses BrowserRouter
✔ SPA behavior (no reload)

4️⃣ App Routing (App.jsx)
import { Routes, Route } from "react-router-dom";
import Navbar from "./components/Navbar";
import Home from "./pages/Home";
import AboutUs from "./pages/AboutUs";
import Todos from "./pages/Todos";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <>
      <Navbar />

      <Routes>
        <Route path="/home" element={<Home />} />
        <Route path="/aboutus" element={<AboutUs />} />
        <Route path="/todos" element={<Todos />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </>
  );
}

export default App;


✔ Navbar visible on all pages
✔ * handles 404 Not Found

5️⃣ Navbar (components/Navbar.jsx)
import { NavLink } from "react-router-dom";

const Navbar = () => {
  return (
    <nav className="navbar">
      <NavLink to="/home">Home</NavLink>
      <NavLink to="/aboutus">About Us</NavLink>
      <NavLink to="/todos">Todos</NavLink>
    </nav>
  );
};

export default Navbar;


✔ Uses NavLink (not <a> tags)
✔ Active styling supported

6️⃣ Pages
Home Page (pages/Home.jsx)
const Home = () => {
  return <h2>This is Home Page</h2>;
};

export default Home;

About Us Page (pages/AboutUs.jsx)
const AboutUs = () => {
  return <h2>This is About Us Page</h2>;
};

export default AboutUs;

7️⃣ Todos Page (API + Grid) (pages/Todos.jsx)
import { useEffect, useState } from "react";
import TodoCard from "../components/TodoCard";

const Todos = () => {
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.json())
      .then((data) => setTodos(data.slice(0, 10)));
  }, []);

  return (
    <div>
      <h2>Todos</h2>
      <div className="todo-grid">
        {todos.map((todo) => (
          <TodoCard key={todo.id} todo={todo} />
        ))}
      </div>
    </div>
  );
};

export default Todos;


✔ Fetches todos
✔ Displays first 10 only
✔ Grid layout

8️⃣ Todo Card Component (components/TodoCard.jsx)
const TodoCard = ({ todo }) => {
  return (
    <div className="todo-card">
      <h4>{todo.title}</h4>
      <p>
        Status:{" "}
        {todo.completed ? "Completed ✅" : "Not Completed ❌"}
      </p>
    </div>
  );
};

export default TodoCard;

9️⃣ 404 Page (pages/NotFound.jsx)
const NotFound = () => {
  return <h2>404 - Page Not Found</h2>;
};

export default NotFound;


✔ Renders for any unknown route

🔟 Styling (index.css)
body {
  font-family: Arial, sans-serif;
  margin: 0;
}

.navbar {
  display: flex;
  gap: 20px;
  padding: 15px;
  background-color: #222;
}

.navbar a {
  color: white;
  text-decoration: none;
}

.navbar a.active {
  font-weight: bold;
  border-bottom: 2px solid white;
}

.todo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 15px;
  padding: 20px;
}

.todo-card {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 6px;
  background: #f9f9f9;
}
