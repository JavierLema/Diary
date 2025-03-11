---
favorited: true
tags: [Start]
title: Very Important Topics
created: '2024-11-18T12:02:37.883Z'
modified: '2025-02-10T10:06:00.461Z'
---

# Very Important Topics

<details>
  <summary>¿Cómo lanzar los mensajes al equipo?</summary>

  Esto es mejorable, <span style="color:darkred">**NUNCA** criticar ni ser alarmista!</span>
  ESto no es prioritario, podemos hacer un refactor en estos puntos (a,b,c ...) y se podría hacer asi:...

</details>

<details>
  <summary>¿Qué hacer un spike y que no hacer en un spike?</summary>

  **Mal creado:** https://ccc.atlassian.net/browse/RFE-17464

  Este ticket pide un spike que basándose en los tickets de seguridad determine si se hizo correctamente o no.

  El documento que creé está completamente fuera de lugar porque:
  - **Va dirigido a negocio y es muy dificil de leer** (comentario de Juan)
  - Los **posibles bugs** encontrados durante la investigación deberían o estar en **un documento aparte** para comentarlo luego con QA.
  - Antes de reportar un posible fallo/error hay que saber si hay algún ticket creado al respecto (tags)

  El excel que está adjunto al ticket sería lo que realmente necesitaría este spike:
  - Ticket de seguridad. Determinar si dónde se implementó se hizo correctamente o si necesita de negocio para decidirlo.

  Y ya estaría.

  **Resumen:** Primero hay que determinar que es lo que quieren que se haga y luego se hace. 

  Una vez entendido, **hacer un guión**.

  **Ejemplo Bueno:** https://docs.google.com/document/d/1PEMhN0WjyNaa70VdhwM0uvh397V2imJ_AW5cCXe34rM/edit?tab=t.0
  
</details>

<details>
  <summary>DashBoard - Deuda técnica</summary>

  Deuda técnica: https://ccc.atlassian.net/jira/dashboards/12024

  - **Filter Results: RFE - Open Architecture and Modernization**
    No se pueden coger si no están estado Open y están estimadas.

  - **Filter Results: RFE - Open Techdebt and Maintenance**
    Mirarla, preguntar al reporter si se puede pillar, mirar si se puede eslicear

  - **Filter Results: RFE - Open Feature Hygiene**
    Pendiente de planificación, deben planificarlo Erik, pero...

  - **Filter Results: RFE - Radu's backlog**
    Solo para saber que está haciendo y por donde va Radu.
    Si algo de ahí podría ser intersante se podría hablar con Radu y crear una nueva tarea.

</details>






