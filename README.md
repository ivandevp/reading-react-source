# Mis notas personales leyendo el código fuente de React

[React](https://reactjs.org/) es uno de mis librerías favoritas de JavaScript,
no solo desde el punto de vista de usuario, sino también desde la ingenería
detrás para obtener el mejor performance posible de aplicaciones como Facebook.

## Estructura del proyecto

Lo primero que llama la atención al entrar al proyecto es que encontramos una
estructura en la que no hay una carpeta `src/` que contenga el código fuente,
si investigamos un poco más, nos daremos cuenta, que todo está dentro de
`packages/` y si buscamos el porqué, nos daremos cuenta que se trata de un
[_monorepo_](https://gomonorepo.org/) administrado por una herramienta creada
por el equipo de Babel, llamada [`Lerna`](https://github.com/lerna/lerna).

### Por dónde empezar

Ok, viendo un poco sobre _Lerna_, a grandes razgos indica ser una herramienta
útil para manejar múltiples paquetes (proyectos) dentro de un mismo repositorio.
Esta herramienta hace buena dupla con [yarn](https://yarnpkg.com/es-ES/) y
viendo un poco sobre las convensiones, el `package.json` debería tener un key
llamado _workspaces_ y su valor debería ser un arreglo con la lista de rutas de
los paquetes.

> TODO: Entender mejor cómo funciona Lerna en conjunto con Yarn.

Revisando el `package.json` en el repositorio de react, encontramos:

```json
{
    ...,
    "workspaces": [
        "packages/*
    ],
    ...
}
```

Esto nos da una primera indicación de que el código fuente puede encontrarse
dentro de la carpeta `./packages`. Si abrimos, dicha carpeta, encontraremos lo
siguiente:

```text
packages/
├── create-subscription/
├── eslint-plugin-react-hooks/
├── events/
├── jest-mock-scheduler/
├── jest-react/
├── react/
├── react-art/
├── react-cache/
├── react-debug-tools/
├── react-dom/
├── react-is/
├── react-native-renderer/
├── react-noop-renderer/
├── react-reconciler/
├── react-stream/
├── react-test-renderer/
├── scheduler/
└── shared/
```

Voilà! Encontramos la primera subcarpeta donde podemos echar un vistazo. ¿Y ahora?
¿Qué carpeta inspeccionamos? Si lo que buscamos entender es React, ¿deberíamos
ver qué contiene la carpeta de React?

Ok, para responder esto, debemos de analizar cuál es nuestro punto de partida
como usuario, de esa manera podremos identificar qué deberíamos buscar entender
primero. Revisemos el siguiente código:

```js
import React from 'react';
import ReactDOM from 'react-dom';

const HelloWorld = () => <h1>Hola mundo!</h1>;

// Asumamos que tenemos un index.html con un <div id="root"></div>
ReactDOM.render(
    <HelloWorld />,
    document.getElementById('root'),
);
```

Viendo el código anterior, ¿nuestro punto de partida es el componente
`<HelloWorld />`? La respuesta es _no_. El punto de partida es cuando se
renderiza el componente dentro del HTML, y eso se logra a través del método
render del paquete importado `react-dom`. Así que podemos asumir lo siguiente:

* La carpeta a revisar primero es `./packages/react-dom`
* El paquete `react-dom` debe exportar un objeto que tenga un método llamado
  `render`, dicho método debe aceptar al menos 2 parámetros.

Con estas premisas asumidas, veamos que contiene el paquete de `react-dom`
:rocket:.