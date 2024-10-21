# Propuesta Técnica para el Desarrollo del Simulador de Crédito - Roda

Esta propuesta técnica describe la infraestructura e arquitectura, tecnologías y procesos involucrados en el desarrollo del Simulador de Crédito de Roda. El sistema estará diseñado para vendedores de la compañía, integrando funciones para microcréditos, motocicletas y eBikes, con conectividad a Airtable y AWS.

## Objetivo General
Desarrollar una aplicación interactiva que permita a los vendedores de Roda gestionar la oferta de créditos, integrándose con Airtable para el envío y recepción de datos, y con AWS para la ejecución de scripts a través de un puerto abierto.


## Requerimientos Funcionales
1. **Usuarios:** Vendedores de la compañía.

2. **Tipos de Crédito Soportados:** Microcrédito, Motocicleta y eBike.

3. **Interactividad:** La aplicación será amigable e intuitiva.

4. **Conectividad con Airtable:**
   - **Enviar Datos:** Capacidad para enviar información al formalizar la compra.
   - **Recibir Datos:** Acceso al catálogo de motocicletas desde Airtable.

5. **Integración con AWS:** Conexión a scripts alojados en AWS a través de un puerto abierto.
<br><br><br>

# Prototipado y Diseño con Figma

Para garantizar una experiencia de usuario óptima, utilizaremos Figma para el diseño y prototipado de la interfaz del Simulador de Crédito. Esta herramienta nos permitirá:

- Diseñar una interfaz intuitiva que satisfaga las necesidades de los vendedores.
- Crear prototipos interactivos que faciliten la visualización del flujo de la aplicación.
- Recoger feedback de los usuarios para realizar ajustes antes del desarrollo.

El uso de Figma nos ayudará a reducir el tiempo de desarrollo y a asegurar que la aplicación sea amigable y efectiva desde el principio.
<br><br><br>

# Tecnologías Clave para el Desarrollo

## Front-End

- **Framework:** React con Nextjs.
    - **Justificación:** Next.js mejora el rendimiento del sitio con renderizado del lado del servidor (SSR) y generación estática (SSG), permitiendo experiencias rápidas y fluidas.

        [Documentación React](https://react.dev/) - 
        [Documentación Next.js](https://nextjs.org/)

- **Librería de Estilos: Tailwind CSS.**
    - **Justificación:** Facilita el desarrollo rápido con un sistema de diseño modular y responsivo.

        [Documentación Tailwind CSS](https://tailwindcss.com/docs/installation)

- **Diseño:**
  - Diseño responsivo para adaptarse a diferentes dispositivos.
  - Tailwindcss.
  - Utilización de componentes reutilizables para facilitar el mantenimiento **(Shadcn)**.  

- **Componentes de UI: Shadcn (Shadcn/ui).**
    - **Justificación:** Proporciona componentes reutilizables, accesibles y fácilmente personalizables para mejorar la experiencia del usuario.

      [Documentación Shadcn / ui](https://ui.shadcn.com/docs/installation/next)


- **Gestión de Estado: Zustand.**
   - **Justificación:** Una librería ligera de gestión de estado global, simple y eficiente.

      [Documentación Zustand](https://zustand.docs.pmnd.rs/getting-started/introduction)



- **Solicitudes HTTP: Axios.**
   - **Justificación:**  Axios será usado para interactuar con la API, gestionar las solicitudes HTTP y manipular datos recibidos y enviados desde Airtable y AWS.

     [Documentación Axios](https://axios-http.com/es/docs/intro)

   

- **Validación de Formularios: React Hook Form.**
   - **Justificación:**  Ofrece validación robusta y eficiente en los formularios, con manejo de errores y estados de los inputs.

     [Documentación React Hook Form](https://www.react-hook-form.com/get-started)
<br><br><br>

## Back-End

- **Servidor: Node.js con Express.js.** Node.js con Express.js para un servidor web ligero y escalable.
   - **Justificación:**  Framework minimalista y de alto rendimiento que permite crear una API RESTful eficiente para las interacciones entre el front-end y servicios como Airtable y AWS.

      [Documentación Nodejs](https://nodejs.org/en/)
  

- **Conexión con Airtable: Airtable API.** Node.js con Express.js para un servidor web ligero y escalable.
   - **Justificación:**  Manejo de operaciones CRUD (crear, leer, actualizar y eliminar) mediante la API de Airtable para gestionar los datos del catálogo y las solicitudes de crédito.

     [Airtable](https://www.airtable.com/)



- **Integración con AWS:** Node.js con Express.js para un servidor web ligero y escalable.
   - **AWS Lambda:**  Ejecutará scripts de forma escalable y sin servidor.
   - **Amazon API Gateway:**  Se usará para exponer de forma segura los endpoints que se conectarán con AWS Lambda.
<br><br><br>


## DevOps y Deploy

Para asegurar un proceso eficiente de despliegue y monitoreo, se implementarán las siguientes tecnologías y procesos:

- **Contenedorización:** Se utilizará **Docker** para crear contenedores consistentes entre los entornos de desarrollo, testing y producción.

- **Pipeline de CI/CD:**

    - **GitHub Actions:** Automatización del proceso de integración y entrega continua, permitiendo ejecutar tests, builds y despliegues de forma automática con cada cambio en el código.

- **Despliegue:**

    - **Frontend:** Despliegue en **Vercel** para aprovechar sus características nativas de serverless y su capacidad para servir páginas estáticas o renderizadas del lado del servidor.

    - **Backend:** Despliegue en AWS EC2, dependiendo de la escalabilidad requerida y el uso intensivo de AWS para las integraciones.

    - **Monitoreo:**

        - **Sentry:** Se utilizará para monitorear errores en tiempo real tanto en el frontend como en el backend, permitiendo un rastreo de fallos eficiente.

          [Sentry](https://sentry.io/welcome/)
        


- **Seguridad**
    - **Autenticación:** JWT (JSON Web Tokens) para asegurar el acceso seguro a la API por parte de los vendedores.

      [JWT](https://jwt.io/)

    

    - **Protocolos de Seguridad:** HTTPS para asegurar la comunicación.

    - **CORS:** Configuración adecuada para limitar el acceso a la API solo a dominios permitidos.
<br><br><br>


# Funcionalidades Principales

1. Selección del Tipo de Crédito
   - El vendedor podrá seleccionar entre Microcrédito, Motocicleta o eBike.

   - **Funcionalidad:** Interfaz que permite seleccionar el tipo de crédito y cargar el catálogo de motocicletas desde Airtable cuando sea necesario.

2. Ingreso de Parámetros del Crédito
   - El vendedor ingresará la periodicidad de pago (semanal, quincenal, mensual) y la tasa de interés aplicable.

   - **Funcionalidad:** Formularios interactivos validados con React Hook Form.

3. Integración con el Catálogo de Motocicletas
   - Si se selecciona "Motocicleta", se mostrará el catálogo desde Airtable.

   - **Funcionalidad:** Axios enviará las solicitudes al backend que accederá a Airtable para obtener el catálogo actualizado.

4. Cálculo de la Cuota
   - Se calcularán las cuotas en función de los parámetros ingresados por el vendedor.

   - **Funcionalidad:** Una calculadora en tiempo real que mostrará los resultados de las cuotas basadas en la tasa de interés y la periodicidad seleccionada.

5. Formalización de la Compra
   - Los datos de la compra serán enviados a Airtable a través de un botón de Enviar.
   - **Funcionalidad:** Axios manejará el envío de datos y mostrará una confirmación visual de que la operación ha sido exitosa, o un error en caso de fallo.
<br><br><br>

# Testing y Aseguramiento de la Calidad

## Pruebas Unitarias y de Integración
- **Jest:** Se utilizarán para crear pruebas unitarias de los componentes del frontend y para pruebas de integración que garanticen la correcta funcionalidad de la aplicación.

   [Jest](https://jestjs.io/docs/getting-started)
<br><br><br>

# Integraciones y Conectividad

## Airtable
- **API RESTful:** Se utilizará para realizar operaciones de lectura y escritura, asegurando que los datos sean transmitidos de manera segura y eficiente.

- **Autenticación:** Tokens de acceso administrados de forma segura.

## AWS
- **Lambda:** Ejecutará scripts alojados en AWS.

- **API Gateway:** Expondrá los endpoints para interactuar con Lambda.
<br><br>

# Despliegue y Monitorización

## Despliegue Continuo
- **Vercel:** Para el despliegue del frontend, aprovechando sus capacidades para manejar proyectos de Next.js de forma eficiente.

- **AWS EC2:** El backend será desplegado en AWS EC2, según las necesidades de escalabilidad.

## Monitorización
- **Sentry:** Para la gestión de errores en tiempo real.
<br><br>

# Conclusión

El Simulador de Crédito de Roda es una herramienta diseñada para facilitar el proceso de créditos para los vendedores. Utilizando tecnologías modernas como React y Node.js, ofreceremos una aplicación más eficiente y fácil de usar.

Con la integración de Airtable y AWS, los vendedores podrán concentrarse en lo esencial: ayudar a los clientes.