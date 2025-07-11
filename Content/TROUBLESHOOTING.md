# Guía de Troubleshooting para la API de GitHub

Esta guía presenta un plan de acción para los errores más comunes al interactuar con la API de GitHub, con el fin de asegurar una extracción de datos robusta y continua.

---

## Error Común 1: 401 Unauthorized

Este es el error más frecuente relacionado con la autenticación. Indica que la API no pudo validar tu identidad.

### Descripción del Problema

La petición es rechazada porque las credenciales proporcionadas son inválidas, incorrectas o no tienen los permisos necesarios.

### Causas Principales y Soluciones

#### Token Inválido o Expirado

**Plan de Acción:**
- **Validar el Token:** Asegurar que el PAT esté activo y no haya sido revocado.
- **Verificar Permisos (Scopes):** Confirmar que el token tiene los permisos necesarios (ej. `repo`).
- **Regenerar si es necesario:** Si el token es inválido, generar uno nuevo desde la configuración de desarrollador de GitHub.

#### Token sin los Permisos Necesarios

**Solución:**
- Asegurarse de que el PAT tenga los *scopes* o permisos adecuados para la acción que se intenta realizar.  
- Para este proyecto, el scope `repo` es suficiente para acceder a la información de repositorios públicos y privados.

#### Error en el Encabezado de Autorización

**Solución:**
- Revisar el código para confirmar que el encabezado `Authorization` se está enviando correctamente.  
- El formato debe ser: `token TU_TOKEN_AQUI`.  
- Un error común es olvidar la palabra `"token"` antes del PAT.

---

## Error Común 2: 403 Forbidden - Límite de Peticiones Excedido

Este error suele estar relacionado con los límites de uso de la API (*Rate Limiting*).

### Descripción del Problema

La API rechaza la petición porque se ha excedido el número de llamadas permitidas en un período de tiempo determinado.

### Causas Principales y Soluciones

#### Uso de Peticiones No Autenticadas

**Causa:**  
Realizar llamadas a la API sin un PAT.  
El límite para peticiones anónimas es muy bajo (aproximadamente 60 por hora).

**Solución:**  
- Implementar siempre la autenticación con un PAT.  
- Esto aumenta el límite a **5,000 peticiones por hora**, lo cual es adecuado para la mayoría de las tareas de extracción de datos.

#### Scripts Muy Agresivos

**Causa:**  
Un script que realiza una cantidad masiva de peticiones en un corto período de tiempo (por ejemplo, al recorrer miles de páginas de resultados sin pausas).

**Solución (Enfoque Proactivo):**
- **Revisar los Headers de la Respuesta:**  
  La respuesta de la API de GitHub incluye encabezados como:
  - `X-RateLimit-Limit` (el límite total)
  - `X-RateLimit-Remaining` (cuántas peticiones quedan)
  - `X-RateLimit-Reset` (cuándo se reinicia el contador)  
  Un script avanzado puede leer estos encabezados y, si el número de peticiones restantes es bajo, esperar un tiempo antes de continuar.

- **Añadir Pausas:**  
  Implementar pequeñas pausas (`time.sleep()`) en los bucles largos para distribuir las peticiones a lo largo del tiempo y evitar agotar el límite rápidamente.