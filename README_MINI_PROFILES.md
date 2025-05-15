
# 📘 React App - Mini Blog de Profils

Cette application React simule un mini blog avec des profils utilisateurs, incluant la navigation, la récupération de données, les paramètres dynamiques, les props, etc.

---

## ⚙️ Technologies et hooks utilisés

- `props` pour transmettre des données entre composants
- `useEffect` pour appeler une API (ou simuler un chargement)
- `useNavigate` pour la redirection
- `useParams` pour lire l'ID dans l'URL
- `useLocation` pour accéder aux infos de navigation
- `Link` et `NavLink` pour la navigation
- `Routes` et `Route` pour gérer les pages

---

## 📁 Structure de l'application

```
src/
├── components/
│   ├── Home.jsx
│   ├── UserList.jsx
│   ├── UserDetails.jsx
│   ├── NotFound.jsx
├── App.jsx
├── index.js
```

---

## 🛠️ Création de l'app

```bash
npx create-react-app mini-profiles-app
cd mini-profiles-app
npm install react-router-dom@6.3.0
```

---

## 🧩 Exemple de code

### `App.jsx`

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./components/Home";
import UserList from "./components/UserList";
import UserDetails from "./components/UserDetails";
import NotFound from "./components/NotFound";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<UserList />} />
        <Route path="/users/:id" element={<UserDetails />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

### `Home.jsx`

```jsx
import { Link, NavLink } from "react-router-dom";

const Home = () => {
  return (
    <div>
      <h1>Bienvenue au Mini Blog</h1>
      <NavLink to="/users">Voir les utilisateurs</NavLink>
    </div>
  );
};

export default Home;
```

### `UserList.jsx`

```jsx
import { useEffect, useState } from "react";
import { Link } from "react-router-dom";

const UserList = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <div>
      <h2>Utilisateurs</h2>
      <ul>
        {users.map(user => (
          <li key={user.id}>
            <Link to={`/users/${user.id}`}>{user.name}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
};

export default UserList;
```

### `UserDetails.jsx`

```jsx
import { useParams, useNavigate, useLocation } from "react-router-dom";
import { useEffect, useState } from "react";

const UserDetails = () => {
  const { id } = useParams();
  const navigate = useNavigate();
  const location = useLocation();
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
      .then(res => res.json())
      .then(data => setUser(data));
  }, [id]);

  if (!user) return <p>Chargement...</p>;

  return (
    <div>
      <h2>Détails de {user.name}</h2>
      <p>Email: {user.email}</p>
      <p>Ville: {user.address.city}</p>
      <p>Chemin actuel : {location.pathname}</p>
      <button onClick={() => navigate(-1)}>Retour</button>
    </div>
  );
};

export default UserDetails;
```

### `NotFound.jsx`

```jsx
const NotFound = () => <h1>404 - Page non trouvée</h1>;
export default NotFound;
```

---

## 🚀 Démarrer le projet

```bash
npm start
```

Ouvre [http://localhost:3000](http://localhost:3000) pour voir l’application.



🔍 Pourquoi id est dans ce tableau ?
Parce que tu veux que le code dans useEffect soit relancé chaque fois que la valeur de id change.

Dans ton app React :

Tu as une route comme /users/:id

Quand tu vas de /users/3 à /users/7, id change

Si tu ne mets pas id dans [ ], le fetch() ne sera pas relancé

Résultat : tu afficheras toujours l’ancien utilisateur

💡 Analogie simple :
Imagine useEffect comme une alarme :

Tu dis : « 🔔 Préviens-moi quand id change »

React : « OK, je relancerai ton code à chaque changement de id »

---
