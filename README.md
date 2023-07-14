Link al curso de React: [REACT DESDE CERO por Sergie Code](https://youtu.be/ladwC6Lrs-M)

# Tutorial para hacer Buscador de Películas en React

Este es un tutorial paso a paso para crear un buscador de películas utilizando React. El buscador obtendrá datos de la API de The Movie Database (TMDb) y mostrará los resultados en pantalla. El proyecto está creado con Vite y el archivo principal se llama "BuscadorPeliculas.jsx".

## Requisitos

Antes de comenzar, asegúrate de tener instalado lo siguiente:

-   Node.js
-   npm (administrador de paquetes de Node.js)

## Pasos

### 1. Crear el proyecto

Para crear el proyecto, ejecuta los siguientes comandos en tu terminal:

```
    npx create-vite buscador-peliculas-react
    cd buscador-peliculas-react
```

### 2. Instalar dependencias

En el directorio del proyecto, ejecuta el siguiente comando para instalar las dependencias necesarias:

```
    npm install react react-dom
```

### 3. Crear el archivo principal

Crea un nuevo archivo llamado "BuscadorPeliculas.jsx" en el directorio "src" y copia el siguiente código:

```
    import { useState } from "react"
    
    export const BuscadorPeliculas = () => {
    
      const urlBase = 'https://api.themoviedb.org/3/search/movie'
      const API_KEY = 'YOUR_API_KEY'
    
      const [busqueda, setBusqueda] = useState('')
      const [peliculas, setPeliculas] = useState([])
    
      const handleInputChange = (e) => {
        setBusqueda(e.target.value)
      }
    
      const handleSubmit = (e) => {
        e.preventDefault()
        fetchPeliculas()
      }
    
      const fetchPeliculas = async () => {
        try {
          const response = await fetch(`${urlBase}?query=${busqueda}&api_key=${API_KEY}`)
          const data = await response.json()
          console.log(data.results)
          setPeliculas(data.results)
        } catch (error) {
          console.error('Ha ocurrido un error: ', error)
        }
      }
    
      return (
        <div className="container">
          <h1 className="title">Buscador de Películas</h1>
          <form onSubmit={handleSubmit}>
            <input
              type="text"
              placeholder="Escribí una película"
              value={busqueda}
              onChange={handleInputChange}
            />
            <button type="submit" className="search-button">Buscar</button>
          </form>
    
          <div className="movie-list">
            {peliculas.map((pelicula) => (
              <div key={pelicula.id} className="movie-card">
                <img src={`https://image.tmdb.org/t/p/w500${pelicula.poster_path}`} alt={pelicula.title} />
                <h2>{pelicula.title}</h2>
                <p>{pelicula.overview}</p>
              </div>
            ))}
          </div>
        </div>
      )
    }

```

### 4. Agregar estilos

Crea un nuevo archivo CSS llamado "styles.css" en el directorio "src" y agrega los siguientes estilos:

```
    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    
    .title {
      font-size: 24px;
      margin-bottom: 20px;
    }
    
    .search-button {
      margin-left: 10px;
    }
    
    .movie-list {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      grid-gap: 20px;
    }
    
    .movie-card {
      background-color: #f5f5f5;
      padding: 10px;
    }
    
    .movie-card img {
      width: 100%;
      height: auto;
      margin-bottom: 10px;
    }
    
    .movie-card h2 {
      font-size: 18px;
      margin-bottom: 5px;
    }
    
    .movie-card p {
      font-size: 14px;
      color: #888;
    }
```

### 5. Renderizar el componente

Abre el archivo "main.jsx" en el directorio "src" y reemplaza su contenido con el siguiente código:

```
    import React from "react";
    import ReactDOM from "react-dom";
    import { BuscadorPeliculas } from "./BuscadorPeliculas";
    import "./styles.css";
    
    ReactDOM.render(
      <React.StrictMode>
        <BuscadorPeliculas />
      </React.StrictMode>,
      document.getElementById("root")
    );

```


## Conclusiones

En este tutorial, aprendiste cómo crear un buscador de películas en React utilizando Vite como herramienta de construcción. El componente `BuscadorPeliculas` realiza solicitudes a la API de The Movie Database para buscar películas según los términos ingresados por el usuario. Los resultados se muestran en una lista con el título, una imagen y una descripción de cada película encontrada.
