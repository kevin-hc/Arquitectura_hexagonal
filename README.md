## Arquitectura hexagonal - Aplicación de gestión de tareas
Esta aplicación es un ejemplo de un sistema de gestión de tareas que sigue la arquitectura hexagonal. La aplicación permite crear, leer, actualizar y eliminar tareas, así como obtener información adicional de una tarea a través de una API externa.

## Arquitectura hexagonal
La arquitectura hexagonal, también conocida como Puertos y Adaptadores, es un patrón de diseño que busca mantener una separación clara de las responsabilidades en una aplicación, facilitando la adaptabilidad, escalabilidad y mantenibilidad del software. La arquitectura se organiza en tres capas principales:

**Dominio:** Esta capa contiene las entidades del dominio, que representan los conceptos clave del negocio y sus relaciones, así como la lógica de negocio asociada. Estas entidades son independientes de la infraestructura y la implementación, lo que permite centrarse en las reglas y restricciones del negocio.

**Aplicación:** Esta capa contiene los casos de uso, que representan las acciones o funcionalidades que la aplicación puede realizar. Los casos de uso coordinan la comunicación entre los puertos de entrada (interfaces que representan las acciones que se pueden realizar desde el exterior) y los puertos de salida (interfaces que representan las acciones que la aplicación puede realizar hacia el exterior, como interactuar con bases de datos o servicios externos).

**Infraestructura:** Esta capa contiene los adaptadores y la implementación de los puertos de salida, así como la configuración y la interacción con servicios externos. Los adaptadores son responsables de convertir las solicitudes externas en llamadas a los casos de uso y de convertir las respuestas de los casos de uso en respuestas comprensibles para los sistemas externos.

## La arquitectura hexagonal se adhiere a los principios SOLID:

**Principio de Responsabilidad Única (SRP)**: Cada capa tiene una responsabilidad única y bien definida, evitando la mezcla de responsabilidades y facilitando el mantenimiento del código.

**Principio de Abierto/Cerrado (OCP)**: Las entidades y los casos de uso están abiertos a la extensión pero cerrados a la modificación. Si se necesita agregar una nueva funcionalidad, se puede hacer extendiendo los casos de uso o creando nuevos adaptadores sin modificar el código existente.

**Principio de Sustitución de Liskov (LSP)**: Los adaptadores y las implementaciones de los puertos deben ser sustituibles sin afectar el comportamiento del sistema, lo que permite cambiar fácilmente entre diferentes implementaciones de infraestructura o servicios externos.

**Principio de Segregación de Interfaces (ISP)**: Los puertos de entrada y salida definen interfaces pequeñas y específicas para cada funcionalidad, lo que facilita la implementación de adaptadores y evita depender de interfaces innecesariamente grandes.

**Principio de Inversión de Dependencias (DIP)**: Las dependencias entre las capas se invierten mediante la inyección de dependencias, permitiendo que las capas de dominio y aplicación dependan de abstracciones en lugar de implementaciones concretas.

## Rutas de la API
A continuación se enumeran las rutas de la API con sus métodos HTTP correspondientes y ejemplos de entrada:

**Crear una tarea**
Método: POST
Ruta: /api/tasks
Input: JSON con la información de la tarea (title, description y completed)
json
Copy code
{
   "title": "Ejemplo de título",
   "description": "Ejemplo de descripción",
   "completed": false
}
Obtener una tarea por ID

**Método: GET**
Ruta: /api/tasks/{taskId}
Input: taskId en la ruta (reemplazar {taskId} con el ID de la tarea que deseas obtener)
Obtener todas las tareas

**Método: GET**
Ruta: /api/tasks
Actualizar una tarea

**Método: PUT**
Ruta: /api/tasks/{taskId}
Input: taskId en la ruta (reemplazar {taskId} con el ID de la tarea que deseas actualizar) y JSON con la información actualizada de la tarea (title, description y completed)
json
Copy code
{
   "title": "Nuevo título",
   "description": "Nueva descripción",
   "completed": true
}
Eliminar una tarea por ID

**Método: DELETE**
Ruta: /api/tasks/{taskId}
Input: taskId en la ruta (reemplazar {taskId} con el ID de la tarea que deseas eliminar)
Obtener información adicional de una tarea

**Método: GET**
Ruta: /api/tasks/{taskId}/additional-info
Input: taskId en la ruta (reemplazar {taskId} con el ID de la tarea para la que deseas obtener información adicional)
Pruebas
Puedes utilizar herramientas como Postman o cURL para probar estas rutas. Asegúrate de que la aplicación esté en ejecución antes de realizar las pruebas.

**Entidades del dominio**
Dentro de la capa de dominio, se definen las entidades del negocio que representan los conceptos clave de la aplicación. En el contexto de esta aplicación de gestión de tareas, podríamos tener la siguiente entidad:

Tarea: Representa una tarea con sus atributos como el título, descripción y estado de completitud.
python
Copy code
class Task:
    def __init__(self, title, description, completed):
        self.title = title
        self.description = description
        self.completed = completed
Casos de uso
Los casos de uso definen las acciones o funcionalidades que la aplicación puede realizar. Estos casos de uso se encuentran en la capa de aplicación y se comunican con los puertos de entrada y salida. Aquí hay algunos ejemplos de casos de uso para la aplicación de gestión de tareas:

Crear tarea: Permite crear una nueva tarea en el sistema.
Obtener tarea por ID: Recupera una tarea específica basada en su ID.
Obtener todas las tareas: Obtiene una lista de todas las tareas registradas en el sistema.
Actualizar tarea: Actualiza los atributos de una tarea existente.
Eliminar tarea: Elimina una tarea del sistema.
Adaptadores de puertos de entrada
Los adaptadores de puertos de entrada se encargan de recibir las solicitudes externas y dirigirlas hacia los casos de uso correspondientes. En el contexto de la aplicación de gestión de tareas, los adaptadores de puertos de entrada podrían ser implementados como controladores de una API REST.

**Adaptadores de puertos de salida**
Los adaptadores de puertos de salida se encargan de interactuar con la infraestructura externa, como bases de datos o servicios externos, en nombre de los casos de uso. En el caso de la aplicación de gestión de tareas, los adaptadores de puertos de salida podrían ser responsables de almacenar y recuperar las tareas en una base de datos.

**Servicios externos**
La aplicación de gestión de tareas también puede interactuar con servicios externos para obtener información adicional sobre las tareas. Por ejemplo, podría conectarse a un servicio de clima para obtener la información meteorológica asociada a una tarea.

**Pruebas de integración**
Es importante realizar pruebas de integración para asegurar el correcto funcionamiento de la aplicación en su conjunto. Estas pruebas verifican que los diferentes componentes de la arquitectura hexagonal interactúen correctamente entre sí y con los servicios externos. Se pueden utilizar herramientas de pruebas como pytest para implementar pruebas de integración.

**Conclusiones**
La arquitectura hexagonal proporciona un enfoque estructurado para el diseño de aplicaciones, fomentando la separación de responsabilidades y facilitando el mantenimiento y escalabilidad del software. Al seguir esta arquitectura, la aplicación de gestión de tareas logra una mayor modularidad, lo que permite realizar cambios y extensiones de manera más sencilla y sin afectar otras partes del sistema.
