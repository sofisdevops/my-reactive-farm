# Cuestionario de React

## 1. ¿Cuál es la diferencia entre un componente presentacional y un componente de página en React? Da ejemplos usando archivos del proyecto.

**Componente presentacional:**

* Se enfoca en *mostrar* información.
* Tiene poca o ninguna logica.
* Solo recibe props y renderiza UI.
* No maneja estados complejos.
* No realiza peticiones.
* Son faciles de reutilizar.

**Ejemplo en el proyecto:**

* `AnimalCard.jsx`: muestra nombre, tipo, edad, peso e imagen del animal. Recibe props y no maneja peticiones ni navegación.
* `Alert.jsx`: muestra mensajes estilizados (Porque tienen: colores e iconos) como *`exito`*, *`error`* o *`info`*.

**Componente de pagina react:**

* Maneja logica, estados, efectos, filtros y peticiones.

**Ejemplo en el proyecto:**

* Carga animales desde MockAPI usando useEffect.
* Tiene estados de loading, error, filtros, busqueda y formulario.
* Renderiza AnimalList, AnimalForm, Alert, Loader, etc.

---

## 2. ¿Para qué se utiliza useState en el proyecto? Menciona dos estados distintos y su función.

`useState` se usa para almacenar valores que cambian mientras la app funciona con la interaccion del usuario o la carga de datos.

#### Dos ejemplos concretos:

* `animals` (en `Farm.jsx`): guarda la lista de animales cargados desde la API.
* `isLoading` (también en `Farm.jsx`): controla si la pagina esta esperando una respuesta del servidor.

Otros estados incluyen: `error`, `search`, y los estados del formulario.

---

## 3. ¿Cómo se usa useEffect para cargar datos desde MockAPI al inicio? Explica el flujo.

El flujo es:

1. Cuando `Farm.jsx` se "monta"(React lo “crea” y lo coloca en el DOM), `useEffect` se ejecuta una sola vez.
2. Dentro del efecto se llama a `getAnimals()` de `animalsApi.js`.
3. Mientras la peticion se procesa, se activa `isLoading = true`.
4. Si la respuesta es exitosa:

   * Se guarda en `animals` con `setAnimals(data)`.
   * Se desactiva `isLoading = false`.
5. Si ocurre un error:

   * Se establece `error` con el mensaje normalizado. (Normalizar un mensaje = convertir cualquier error en un formato claro y comprensible.)
   * También `isLoading = false`.

Esto permite que la UI muestre mensajes adecuados mientras se espera la carga.

---

## 4. ¿Cómo maneja el proyecto los estados de loading, error y lista vacía? ¿Qué se muestra al usuario en cada caso?

* **Loading:**

  * Se muestra un `<Alert variant="info">Cargando animales...</Alert>` cuando se estan cargando los animales.

* **Error:**

  * Muestra un `<Alert variant="error">` si la API falla.

* **Lista vacia:**

  * Si no hay resultados (ya sea porque no existen animales o no coinciden con la busqueda), se muestra:

    * "No hay animales en la granja" o
    * "No se encontraron coincidencias".

Cada estado tiene un mensaje claro para el usuario, lo que mejora la experiencia.

---

## 5. ¿Qué significa que un formulario sea controlado en React? Relaciónalo con el formulario del proyecto.

Un formulario controlado es aquel donde:

* Cada input usa un state para su valor.
* Cada cambio se refleja con onChange en React.

El componente controla totalmente lo que escribe el usuario.

Es decir:

* El valor del input viene de un `useState`.
* Cualquier cambio del usuario dispara `onChange` para actualizar ese estado.

**En este proyecto:**

* El formulario para agregar animales (dentro de `Farm.jsx`) es 100% controlado.
* Inputs como `name`, `type`, `age` o `weight` dependen del estado `formData`.

Esto permite validar, limpiar, deshabilitar botones y manejar el envio.
---

## 6. ¿Por qué es buena práctica separar la lógica de datos en archivos como animalsApi.js en vez de hacer peticiones dentro de los componentes?

Razones:

* **Mantiene los componentes limpios y fáciles de entender.**
* **Evita duplicacion de codigo** (todas las paginas usan la misma funcion `getAnimals`).
* **Facilita pruebas**, ya que se puede mockear la API sin renderizar un componente.
* **Estructura mas ordenada**: los componentes se encargan de UI y los servicios se encargan de datos.

---

## 7. ¿Qué hace que AnimalCard sea un componente reutilizable? ¿Cómo se podría usar una tarjeta similar en otro contexto?

* Acepta props (nombre, tipo, edad, peso, imagen) en lugar de contenido fijo.
* No depende de estados externos.
* No hace peticiones.

Por eso podria usarse en otros contextos, por ejemplo:

* Una **tienda de mascotas** mostrando tarjetas de productos.
* Una **veterinaria**.
* Un **spa de mascotas** donde cada tarjeta representa un recurso diferente.

---

## 8. ¿Qué elementos del proyecto contribuyen a la accesibilidad? Menciona tres y explica su importancia.

Tres importantes dentro del proyecto:

1. **`aria-live` en Alert.jsx**

   Permite que lectores de pantalla anuncien un error o notificacion.

2. **Botón con `aria-label` para cerrar alertas**

   Ayuda a usuarios con lectores de pantalla.

3. **Modo oscuro accesible**

   * Usa colores con contraste adecuados y soporta preferencia del sistema (`prefers-color-scheme`).

Otros detalles como el uso de `role="alert"` y etiquetas en formularios también suman.

---

## 9. Antes de agregar una funcionalidad nueva, ¿qué pasos debes pensar según la filosofía de React? (ej.: qué datos, qué estado, dónde vive la lógica)

React recomienda planear:

1. **Identificar qué datos necesito.**
2. **Decidir qué componente debe tener el estado.**
3. **Pensar qué componentes solo mostrarán información.**
4. **Cómo fluirá la información (props).**
5. **Si necesito efectos (useEffect) o peticiones externas.**

* Este proceso asegura que la UI sea predecible y fácil de mantener.

---

## 10. Conceptos de React reutilizables en cualquier aplicación

1. **Componentes reutilizables** (AnimalCard, Alert, Loader).
2. **useState:** para manejar formularios, filtros o contadores.
3. **useEffect:** cargar datos de los APIs.
4. **Separación entre UI y logica** usando servicios como animalsApi.js.
5. **Props:** pasar información de padres a hijos.

---
*Sofia Ballen*
