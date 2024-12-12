**Diseño de arquitectura**

Tenemos que implementar una arquitectura para exponer un API (B2B), de una solución de AI en Azure, con las siguientes características:

-   Hay un pre-procesado de cada petición que consulta servicios externos (Google Maps entre otros) que tarda 2 segundos de media.
-   Dentro del preprocesado también hay que consultar una BD (que hay que almacenar en la misma solución) con 150M de registros que almacena los límites de cada finca (catastro).
-   Existe un modelo de Computer Vision que tarda 10 segundos de media en inferir un resultado.
-   Hay un post-procesado que implementa diferentes lógicas de negocio a los resultados de la inferencia y que tarda 3 segundos de media.
-   Todo el proceso debe dejar un log para mostrar unas estadísticas mensuales de tiempos, número de peticiones, errores, etc.
-   Además, tenemos que montar un servicio de monitorización que periódicamente valide que todo el End-to-end, enviando una petición prefijada de la cual conocemos el resultado, y si el resultado no es el correcto, no se recibe respuesta o supera un timeout determinado se cree una incidencia en JIRA.
-   Asimismo, tienen que implementarse algún tipo de alertas en Azure que nos avisen si algún servicio se degrada o deja de funcionar correctamente.
-   Se llevarán a cabo 2M de peticiones al año, con picos puntuales de concurrencia de 50 peticiones por segundo en los meses de marzo, abril y mayo, y valles el resto de los meses de 1-2 peticiones por segundo.
-   Los JSONs con los resultados de cada petición y las imágenes resultantes se guardarán en un almacenamiento seguro. Los pesos de cada JSONs van de 5KB a 30KB y el de cada imagen de 400KB a 1MB.
-   Este API se compartirá entre varios clientes, por lo que es importante tener control sobre el acceso de cada uno y el uso (volumen de peticiones) que hace del API por cuestiones de facturación (Quota).

**Nos gustaría que nos describieses que arquitectura utilizarías teniendo en cuenta los siguientes apartados:**

**Infraestructura y Servicios:**

-   Diseña la infraestructura en Azure usando servicios PaaS donde sea posible.
-   Propone una solución de base de datos que permita escalabilidad y rendimiento.
-   Incorpora servicios de Azure que permitan monitorización y telemetría.
-   Incluye donde albergarias la ejecución del modelo de IA.

**Escalabilidad:**

-   Diseña la arquitectura garantizando que pueda manejar picos de carga, especialmente durante fechas indicadas.
-   Propone estrategias de escalado automático basadas en métricas relevantes.

**Seguridad:**

-   Describe cómo asegurarías la aplicación y la infraestructura asociada.
-   Diseña una estrategia de autenticación y autorización.
-   Considera soluciones para proteger la aplicación contra amenazas comunes (e.g., DDoS).

**Despliegue Continuo:**

-   Explica como diseñarías un pipeline de CI/CD utilizando Azure DevOps para la aplicación .NET.
-   Asegura que el proceso de despliegue sea seguro y eficiente.

**Costo:**

-   Proporciona una estimación aproximada del costo mensual de la solución en Azure.
-   Propone estrategias para la optimización de costos.

**Documentación:**

-   Crea un documento que describa la arquitectura propuesta, incluyendo un diagrama visual.
-   Justifica las decisiones tomadas en cada paso y cómo abordan los requerimientos y desafíos de "TechSolutions".

Te adjunto un diagrama de secuencia sencillo para que te hagas una idea del funcionamiento.
