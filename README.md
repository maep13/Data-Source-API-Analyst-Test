Tarea de Proyecto: Analista de Fuente de Datos - Improvado
Este documento detalla el proceso, enfoque y ejecución de la tarea asignada para la posición de Analista de Fuente de Datos. El objetivo es demostrar las habilidades en investigación de APIs, extracción de datos y documentación técnica.
1. Propósito del Proyecto
El objetivo principal es simular un requerimiento de cliente para extraer datos específicos desde la API pública de GitHub. El proyecto busca evaluar las siguientes competencias:
●	Investigación de APIs: La capacidad para navegar documentación técnica y entender la lógica de endpoints, autenticación, paginación y límites.
●	Extracción de Datos: El uso de herramientas técnicas para realizar llamadas a la API y obtener los datos solicitados.
●	Documentación y Troubleshooting: La habilidad para documentar el proceso de manera clara y anticipar posibles problemas y sus soluciones.
2. Enfoque y Herramientas
Para esta tarea, se ha decidido utilizar Google Colab con Python como herramienta principal para la extracción de datos. Esta elección se basa en los siguientes puntos:
●	Potencia y Flexibilidad: A diferencia de herramientas con interfaz gráfica como Postman, Python permite un control total sobre la lógica de extracción, el manejo de errores complejos, la paginación y la transformación de datos.
●	Buenas Prácticas: Permite implementar prácticas de seguridad, como el manejo de tokens de autenticación a través de "Secrets", evitando exponer información sensible directamente en el código.
●	Requerimiento de la Tarea: La propia descripción de la tarea indica que el uso de Google Colab otorgará puntos extra, demostrando una mayor aptitud técnica.
El flujo de trabajo se organizará a través de este repositorio de GitHub, que servirá como centro de toda la documentación y los entregables.
3. Plan de Trabajo - Día 1 (Jueves)
El objetivo de hoy es establecer las bases del proyecto, asegurando que toda la estructura y la investigación preliminar estén completas antes de comenzar con el desarrollo.
Paso 1: Creación del Repositorio en GitHub
●	Acción: Crear un nuevo repositorio público en GitHub.
●	Nombre: Data-Source-API-Analyst-Test
●	Descripción: "Homework assignment for Data Source API Analyst role."
●	Resultado: El repositorio está creado y accesible públicamente.
Paso 2: Estructura del Proyecto
●	Acción: Clonar el repositorio en local y crear la estructura de carpetas requerida.
●	Estructura:
/
├── Content/
├── Postman_Collection/
└── README.md

●	Resultado: La estructura de carpetas y este archivo README.md son subidos al repositorio en el primer commit.
Paso 3: Investigación de la API de GitHub
●	Acción: Consultar la documentación oficial de la API REST de GitHub para identificar los endpoints necesarios.
●	Endpoints a Investigar:
1.	Search Repositories: Para buscar repositorios públicos.
2.	Commits: Para listar los commits de un repositorio.
3.	Contents: Para obtener el contenido de un repositorio.
●	Conceptos a Entender: Lógica de paginación (parámetros per_page y page), y los límites de peticiones (Rate Limits) para usuarios autenticados y no autenticados.
●	Resultado: Comprensión clara de las URLs y parámetros necesarios para las llamadas a la API.
Paso 4: Generación de Credenciales
●	Acción: Crear un "Personal Access Token" (PAT) en la configuración de desarrollador de GitHub.
●	Permisos: Se otorgarán permisos de public_repo para asegurar el acceso a la información pública necesaria.
●	Resultado: Un token de autenticación generado y guardado de forma segura para su uso posterior.
Paso 5: Configuración del Entorno de Desarrollo
●	Acción: Crear un nuevo notebook en Google Colab.
●	Configuración de Seguridad: El PAT generado en el paso anterior se almacenará utilizando la funcionalidad de "Secrets" (secreto) de Google Colab bajo el nombre GITHUB_TOKEN.
●	Resultado: Un entorno de desarrollo listo para empezar a escribir el código de extracción, con las credenciales cargadas de forma segura.
