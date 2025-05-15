
⚙️ Configuration
Pour établir la configuration des routes, il est nécessaire d’importer et d’utiliser trois composants principaux :

<BrowserRouter /> entoure toute l’application et établit la communication avec le serveur.

<Routes /> regroupe toutes les routes et, en cas d’événement, détermine laquelle doit être suivie.

<Route /> représente une route et le composant qui sera affiché, en utilisant les attributs path et element.



# 📘 Projet React - Démo de Routage

Ce projet est une application de base en React créée avec **Create React App**. Il servira de point de départ pour explorer le routage avec `react-router-dom`.

## Exercice1

Le projet a été généré avec la commande suivante :

```bash
npx create-react-app demo-routing

import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
    
    </div>
  );
}

export default App;

cd demo-routing
npm start
```

## Exercice2

Installation de react-router-dom :

```bash
npm install react-router-dom@6.3.0
```
## Exercice3

Création d’un composant `Home.jsx` :

Dans le dossier `src/components`, crée un fichier `Home.jsx` et ajoute le code suivant :

```jsx
const Home = () => {
  return(
    <h1>Este es el componente Home</h1>
  );
}

export default Home;


## Exercice4

Configuration de la navigation avec React Router DOM.

Dans le fichier `App.js`, remplace le contenu par le code suivant :


import logo from './logo.svg';
import './App.css';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './components/Home';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Home />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;

## Exercice5

Création d’un composant `About.jsx`.

Dans le dossier `src/components`, crée un fichier `About.jsx` et ajoute le code suivant :


const About = () => {
  return (
    <>
      <h1>Este es el componente About</h1>
      <p>Estamos aprendiendo Routing</p>
    </>
  );
};

export default About;

## Exercice6

Ajout de la route `/about` dans le fichier `App.js` :


import logo from './logo.svg';
import './App.css';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about' element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;


## Exercice7

Création du composant `Profile.jsx`.

Dans le dossier `src/components`, crée un fichier `Profile.jsx` et colle ce code :

const Profile = () => {
  return(
    <div>
      <h1>Este es el perfil de la webster</h1>
      <h2>Cohorte: FT34a</h2>
    </div>
  );
};

export default Profile;

## Exercice8

Ajout de la route `/profile` dans le fichier `App.js` :


import logo from './logo.svg';
import './App.css';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Profile from './components/Profile';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about' element={<About />} />
        <Route path='/profile' element={<Profile />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;

## Exercice9

Création du composant `Person.jsx`.

Dans le dossier `src/components`, crée un fichier `Person.jsx` et ajoute le code suivant :

const Person = () => {
  return (
    <div>
      <h1>Cohorte: FT-34a</h1>
      <label>Instructor:  Webster ❤️</label>
      <p>Alumnos: Los mejores d WL 😎</p>
    </div>
  );
};

export default Person;

## Exercice10

Ajout d’une sous-route `/profile/person` dans `App.js`.

Voici le code complet utilisé :



import logo from './logo.svg';
import './App.css';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Profile from './components/Profile';
import Person from './components/Person';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about'  element={<About />} />
        <Route path='/profile' element={<Profile />} />
        <Route path='/profile/person' element={<Person />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;


## Exercice11

Implémentation des **routes imbriquées** avec React Router.

Dans `App.js`, la route `/person` est maintenant imbriquée sous `/profile`. Voici le code :


import logo from './logo.svg';
import './App.css';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Profile from './components/Profile';
import Person from './components/Person';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about'  element={<About />} />
        <Route path='/profile' element={<Profile />}>
          <Route path=':person' element={<Person />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

export default App;

------

🧭 Navigation
Une fois les routes configurées, l’étape suivante consiste à incorporer des composants qui permettent de naviguer dans toute la page :

<Link /> est équivalent à un élément <a> en HTML.

<NavLink /> est similaire au précédent, avec la différence qu’il permet de modifier les styles du lien lorsqu’il est actif.


# 📘 Composant Home.jsx — Navigation avec Link et NavLink

Ce composant React affiche un titre et deux éléments de navigation permettant de se déplacer vers les routes `/about` et `/profile`.

---

## 📄 Code utilisé


import { Link, NavLink } from 'react-router-dom';

const Home = () => {
  return (
    <>
      <h1>Este es el componente Home</h1>

      <button>
        <Link to='/about'>ABOUT</Link>
      </button>

      <NavLink
        to='/profile'
        style={({ isActive }) =>
          isActive ? { backgroundColor: 'red' } : { backgroundColor: 'blue' }
        }
      >
        Profile
      </NavLink>
    </>
  );
};

export default Home;


# 📘 Composant Profile.jsx — Navigation interne avec Link et Outlet

Ce composant `Profile` affiche un profil personnalisé, ainsi que deux liens :
- Un lien vers une sous-route `"person"`
- Un lien de retour vers la racine `/`

Il utilise aussi `Outlet` pour permettre l'affichage de la sous-route.

---

## 📄 Code utilisé


import { Link, Outlet } from 'react-router-dom';

const Profile = () => {
  return(
    <div>
      <h1>Este es el perfil de la Daianeta 😎</h1>
      <h2>Cohort React</h2>

      <button>
        <Link to='person'>Person</Link>
      </button>

      <button>
        <Link to='/'>Home</Link>
      </button>

      <Outlet />
    </div>
  );
};

export default Profile;


import { useState, useEffect } from "react";

const Person = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <div>
      <h1>Cohorte: FT-34a</h1>
      <label>Instructora: Webster ❤️</label>
      <p>Alumnos: Los mejores de Henry 😎</p>
      <hr />
      <h2>Users:</h2>
      <ul>
        {users.map((user) => {
          return <li key={user.id}>{user.name}</li>;
        })}
      </ul>
    </div>
  );
};

export default Person;


import { useNavigate, useLocation } from "react-router-dom";

const About = () => {
  const navigate = useNavigate();
  const location = useLocation();

  const goToProfile = () => {
    navigate('/profile');
  };

  console.log("Chemin actuel :", location.pathname);

  return (
    <>
      <h1>Composant About</h1>
      <p>Nous sommes sur : {location.pathname}</p>

      <button onClick={goToProfile}>Aller vers le profil</button>
    </>
  );
};

export default About;

Résumé
✅ Tu navigues d’une page à une autre avec navigate('/profile')

✅ Tu récupères le chemin actuel avec useLocation().pathname

