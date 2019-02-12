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

