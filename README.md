# Copilot Studio Credits Monitor

![Version](https://img.shields.io/badge/version-1.0-5552B4)
![Application](https://img.shields.io/badge/application-static%20SPA-FFC000)
![Authentication](https://img.shields.io/badge/authentication-Microsoft%20Entra%20ID-3895FF)
![Processing](https://img.shields.io/badge/data%20processing-in%20browser-BD47BD)
![Exports](https://img.shields.io/badge/exports-PDF%20%7C%20CSV-27B8C6)
![Toolkit](https://img.shields.io/badge/CoE-Toolkit-5552B4)

A browser-based, read-only reporting tool for reviewing Microsoft Copilot Studio credit capacity, environment assignments, and agent inventory through supported Microsoft Power Platform APIs. The application runs as a static Single-Page Application on GitHub Pages, uses delegated Microsoft Entra ID authentication, keeps functional data in browser memory, and requires no backend or database.

**Public version: 1.0**

[Español](#español) · [English](#english)

---

## About this project

**Copilot Studio Credits Monitor** provides a consolidated, tenant-level view of Microsoft Copilot Studio capacity without introducing a custom data platform, scheduled process, or unsupported extraction mechanism.

The tool is designed for Power Platform administrators, Copilot Studio administrators, Center of Excellence teams, solution architects, licensing stakeholders, and governance leads who need a lightweight way to review current capacity and related inventory directly from a browser.

The application retrieves information only when an authorised user signs in. It combines current tenant capacity, environment allocation information, Power Platform environments, and Copilot Studio agent inventory into one bilingual interface.

### What Copilot Studio Credits Monitor provides

The tool supports:

- purchased, allocated, and consumed capacity at tenant level;
- indicative remaining capacity and unallocated capacity;
- selection of an individual capacity type;
- an **All capacity types** option with a transparent per-type breakdown;
- current capacity assignments by environment;
- Power Platform environment inventory;
- Copilot Studio agent inventory by environment;
- local CSV exports for environments and agents;
- local generation of an executive PDF report;
- a built-in test mode with fictional data;
- a downloadable static sample report;
- Spanish and English user interfaces;
- responsive use across desktop, tablet, and mobile devices;
- CoE Toolkit branding, related tools, books, and author information.

Consumption attribution to individual agents is intentionally outside the current scope because the application uses only publicly documented and supported Microsoft APIs.

### Supported data sources

The application uses delegated permissions for the Microsoft Power Platform API:

| Permission | Purpose |
|---|---|
| `Licensing.Allocations.Read` | Read tenant capacity and environment allocations |
| `EnvironmentManagement.Environments.Read` | Read Power Platform environments |
| `ResourceQuery.Resources.Read` | Query Power Platform inventory, including Copilot Studio agents |

The application does not use undocumented Power Platform Admin Center endpoints, browser scraping, desktop automation, or inferred consumption based on transcripts.

### Capacity-type consolidation

Microsoft may return more than one capacity type. The application allows users to inspect each type separately or select **All capacity types**.

The consolidated view performs an arithmetic aggregation of the values returned by Microsoft and always preserves the per-type breakdown for traceability. Because different capacity types may represent different commercial or technical units, the consolidated total should be interpreted as a convenience view rather than a replacement for the detailed breakdown.

### Executive PDF report

The application can generate an executive PDF report directly in the browser.

Depending on the information available, the report includes:

- report scope and generation metadata;
- tenant-level capacity indicators;
- capacity-type breakdown;
- operational signals;
- environment assignments;
- Copilot Studio agent inventory;
- data limitations and interpretation notes;
- related CoE Toolkit tools;
- related books;
- the author’s LinkedIn profile.

The generated report is downloaded by the user and is not uploaded to or retained by the application.

A static example is included in the repository:

[Download the sample PDF report](assets/reports/Copilot_Studio_Credits_Monitor_Sample_Report_v1.0.pdf)

### Test mode

The built-in test mode allows the complete user experience to be reviewed without Microsoft Entra authentication or access to a Power Platform tenant.

Test mode:

- uses fictional data;
- does not request tokens;
- does not call Microsoft APIs;
- completes the capacity, environment, and agent views;
- supports language switching;
- enables CSV and PDF export testing;
- can be opened from the home screen or through `?test=1`.

Example:

```text
https://your-account.github.io/your-repository/?test=1
```

### Privacy by design

Copilot Studio Credits Monitor has no backend and no application database.

Functional report data is held in browser memory for the active session and is removed when the page is reloaded, the session is closed, or the user signs out.

The optional **Remember configuration** setting stores only:

- the public Application (Client) ID;
- the public Directory (Tenant) ID.

The application may also retain the selected interface language locally. Access tokens remain under the control of the Microsoft Authentication Library. Tenant capacity, environments, agents, and generated reports are not persisted by the application.

> Copilot Studio Credits Monitor is an administrative visibility aid. It does not replace Microsoft licensing records, procurement controls, financial reconciliation, security review, privacy review, or formal governance processes.

---

# Español

## Descripción

**Copilot Studio Credits Monitor** es una aplicación web de solo lectura destinada a consultar y presentar la capacidad de Microsoft Copilot Studio, las asignaciones actuales por entorno y el inventario de agentes del tenant.

La solución se ejecuta como una SPA estática alojada en GitHub Pages. La autenticación se realiza mediante Microsoft Entra ID y MSAL utilizando permisos delegados. No requiere backend, base de datos, secretos de aplicación, procesos programados ni infraestructura adicional.

Está orientada a:

- administradores de Power Platform;
- administradores de Copilot Studio;
- líderes y miembros de Centros de Excelencia;
- arquitectos de soluciones;
- responsables de licenciamiento y capacidad;
- equipos de gobierno y operaciones;
- responsables de seguimiento financiero o de adopción.

La herramienta centraliza datos actuales procedentes de APIs públicas y soportadas de Microsoft. No intenta atribuir consumo a agentes individuales ni utiliza mecanismos no documentados para obtener información adicional.

## Objetivo

El objetivo principal es ayudar a una organización a responder preguntas como:

> ¿Cuánta capacidad de Copilot Studio ha adquirido el tenant, cuánto se ha asignado, cuánto se ha consumido y cómo se distribuyen las asignaciones actuales entre los entornos?

También permite responder:

- ¿Qué tipos de capacidad devuelve Microsoft para el tenant?
- ¿Cuál es la capacidad indicativa restante?
- ¿Cuánta capacidad permanece sin asignar?
- ¿Qué entornos tienen una asignación explícita?
- ¿Qué entornos no tienen una asignación explícita registrada?
- ¿Cuántos agentes de Copilot Studio aparecen en el inventario?
- ¿En qué entornos se encuentran esos agentes?
- ¿Cuándo se actualizaron por última vez los datos presentados?

## Cómo funciona

La aplicación utiliza un flujo sencillo y completamente ejecutado en el navegador.

### Configuración de la aplicación

En la pantalla inicial, el usuario introduce:

- **Application (Client) ID**;
- **Directory (Tenant) ID**.

Ambos identificadores son públicos y se validan como GUID antes de iniciar la autenticación. La URI de redirección se calcula dinámicamente a partir de la URL publicada en GitHub Pages.

La opción de recordar la configuración guarda únicamente esos dos identificadores públicos. No guarda datos del reporte.

### Autenticación

La aplicación utiliza Microsoft Entra ID y MSAL para autenticar al usuario mediante Authorization Code Flow con PKCE.

No se utiliza:

- client secret;
- certificado;
- identidad administrada;
- cuenta técnica almacenada en el repositorio.

El usuario ve únicamente la información que sus roles y permisos le permiten consultar.

### Consulta de capacidad

La aplicación consulta los reportes de capacidad del tenant y presenta:

- capacidad adquirida;
- capacidad asignada;
- capacidad consumida;
- capacidad indicativa disponible;
- capacidad sin asignar;
- porcentaje de consumo;
- fecha de la última actualización informada por Microsoft.

### Tipos de capacidad

Cuando Microsoft devuelve varios tipos de capacidad, el usuario puede seleccionar:

- un tipo individual;
- **Todas las capacidades**.

La opción consolidada suma los valores disponibles y mantiene un desglose por tipo. Debido a que distintos tipos pueden representar unidades diferentes, la aplicación muestra una advertencia de interpretación y no oculta los valores originales.

### Asignaciones por entorno

Para cada entorno, la aplicación intenta consultar la asignación actual de capacidad.

Cuando Microsoft devuelve `404 Not Found` para un entorno sin registro de asignación explícita, la aplicación lo interpreta como una asignación disponible de `0` en lugar de bloquear todo el reporte.

Los errores reales de autenticación, permisos, red o servicio continúan visibles para facilitar el diagnóstico.

### Inventario de entornos y agentes

La aplicación obtiene:

- inventario de entornos de Power Platform;
- inventario de agentes de Copilot Studio;
- relación entre agente y entorno cuando la API proporciona la información necesaria.

El inventario se utiliza con fines administrativos y de gobierno. No representa una atribución del consumo de créditos a cada agente.

### Modo de prueba

La pantalla inicial permite abrir un modo de prueba sin autenticación.

Este modo:

- utiliza datos ficticios;
- no solicita tokens;
- no llama a APIs de Microsoft;
- muestra todas las páginas funcionales;
- permite probar filtros, traducciones y diseño responsive;
- permite generar el reporte PDF;
- permite descargar el reporte estático de muestra.

También puede abrirse añadiendo:

```text
?test=1
```

## Estructura de la aplicación

### 1. Pantalla inicial

Incluye:

- identidad visual de CoE Toolkit;
- versión pública;
- perfil de LinkedIn del autor;
- selector de idioma ES/EN;
- campos de Client ID y Tenant ID;
- URI de redirección calculada;
- opción de recordar únicamente la configuración pública;
- acceso al modo de prueba;
- descarga del reporte de muestra;
- información de privacidad y configuración.

### 2. Resumen

Presenta:

- indicadores principales de capacidad;
- selector de tipo de capacidad;
- desglose por tipo;
- señales operativas;
- fecha y estado de actualización;
- acciones de exportación y generación de reporte.

### 3. Entornos

Presenta:

- nombre e identificador del entorno;
- tipo y región cuando están disponibles;
- estado;
- capacidad asignada;
- porcentaje de la asignación total;
- número de agentes relacionados;
- filtros, búsqueda y exportación CSV.

### 4. Agentes

Presenta:

- nombre del agente;
- identificador;
- entorno;
- estado;
- fechas y otros metadatos cuando están disponibles;
- búsqueda, filtros y exportación CSV.

### 5. Acerca de los datos

Explica:

- fuentes utilizadas;
- permisos requeridos;
- alcance de la información;
- tratamiento de asignaciones sin registro explícito;
- limitaciones del consolidado;
- ausencia de consumo por agente;
- privacidad y funcionamiento sin persistencia.

## Qué recibe el usuario

La aplicación proporciona:

- una vista administrativa actual del tenant;
- indicadores de capacidad;
- desglose por tipo de capacidad;
- asignaciones actuales por entorno;
- inventario de entornos;
- inventario de agentes;
- exportaciones CSV locales;
- un reporte ejecutivo PDF;
- un modo de prueba completo;
- un reporte estático de muestra;
- navegación hacia otras herramientas de CoE Toolkit.

## Reporte PDF

El reporte se genera localmente en el navegador y está alineado con el estándar visual de los reportes ejecutivos del CoE Toolkit.

Incluye, según los datos disponibles:

- portada y metadatos;
- resumen ejecutivo;
- alcance del reporte;
- indicadores de capacidad;
- señales operativas;
- desglose por tipo de capacidad;
- entornos con asignación;
- distribución de agentes;
- apéndice de entornos;
- apéndice de agentes;
- limitaciones de los datos;
- herramientas relacionadas;
- libros relacionados;
- autor y perfil de LinkedIn.

El PDF se descarga directamente al dispositivo del usuario. La aplicación no conserva una copia.

Reporte de muestra:

[Descargar reporte PDF de muestra](assets/reports/Copilot_Studio_Credits_Monitor_Sample_Report_v1.0.pdf)

## Exportaciones CSV

Las vistas de entornos y agentes pueden exportarse como archivos CSV.

Las exportaciones:

- se generan en el navegador;
- reflejan los datos y filtros disponibles en la sesión;
- no se envían a un servidor de la aplicación;
- no son almacenadas por la herramienta.

La aplicación no incluye exportación JSON de datos funcionales.

## Privacidad y tratamiento de datos

Copilot Studio Credits Monitor no dispone de backend ni base de datos.

Durante una sesión autenticada, el navegador se comunica directamente con:

- Microsoft Entra ID para autenticación;
- Microsoft Power Platform API para consultar capacidad, entornos, asignaciones e inventario.

La información funcional permanece en memoria y se elimina al recargar, cerrar la página o cerrar sesión.

Opcionalmente pueden almacenarse localmente:

- Application (Client) ID;
- Directory (Tenant) ID;
- idioma seleccionado.

No se almacenan automáticamente:

- créditos adquiridos, asignados o consumidos;
- entornos;
- agentes;
- respuestas completas de las APIs;
- reportes generados;
- históricos;
- snapshots;
- credenciales o secretos.

## Qué no hace la herramienta

La aplicación no:

- atribuye consumo de créditos a agentes individuales;
- obtiene consumo por tema, acción, herramienta o conversación;
- utiliza endpoints internos o no documentados de PPAC;
- realiza scraping del portal de administración;
- estima consumo a partir de transcripciones;
- conserva históricos entre sesiones;
- genera alertas programadas;
- modifica asignaciones de capacidad;
- sustituye los registros oficiales de Microsoft;
- sustituye procesos financieros, de licenciamiento o de gobierno.

## Arquitectura técnica

La solución utiliza:

- HTML, CSS y JavaScript compilados como SPA estática;
- GitHub Pages para hosting;
- Microsoft Entra ID;
- `@azure/msal-browser` para autenticación;
- Microsoft Power Platform API;
- generación local de PDF;
- generación local de CSV;
- estado funcional únicamente en memoria.

Flujo simplificado:

```text
Usuario
  │
  ▼
GitHub Pages SPA
  │
  ├── Microsoft Entra ID / MSAL
  │
  └── Microsoft Power Platform API
          ├── Capacidad tenant
          ├── Asignaciones por entorno
          ├── Entornos
          └── Inventario de agentes
```

## Permisos y APIs

La App Registration debe configurarse como **Single-page application** y utilizar permisos delegados.

Permisos requeridos:

```text
Licensing.Allocations.Read
EnvironmentManagement.Environments.Read
ResourceQuery.Resources.Read
```

La organización puede requerir consentimiento administrativo según sus políticas.

La aplicación no debe configurarse con client secret porque cualquier secreto incluido en un repositorio o bundle de GitHub Pages sería visible para los usuarios.

## Estructura del repositorio

```text
/
├── index.html
├── README.md
├── LICENSE
├── .nojekyll
├── TEST-REPORT.md
│
├── assets/
│   ├── icons/
│   ├── images/
│   │   ├── books/
│   │   └── tools/
│   ├── reports/
│   ├── *.css
│   └── *.js
│
├── docs/
│   ├── DEPLOYMENT.md
│   └── TESTING.md
│
└── tests/
    ├── static-validation.json
    ├── browser-flow-results.json
    └── sample-download-results.json
```

El paquete de publicación no incluye código fuente, `node_modules`, workflows, archivos temporales ni herramientas de compilación.

## Dependencias externas

La aplicación se comunica con servicios de Microsoft para autenticación y lectura de datos.

También puede cargar recursos necesarios para la experiencia visual y generación de reportes según la configuración del bundle publicado.

Los enlaces externos a libros, herramientas y LinkedIn se abren únicamente cuando el usuario los selecciona.

## Uso local

### Abrir el modo de prueba

El contenido estático puede servirse con cualquier servidor HTTP local.

Ejemplo con Python:

```bash
python -m http.server 8080
```

Después, abrir:

```text
http://localhost:8080/?test=1
```

### Probar autenticación local

Para autenticación real, la URL local debe registrarse también como Redirect URI de tipo SPA en Microsoft Entra ID.

Ejemplo:

```text
http://localhost:8080/
```

No se recomienda abrir `index.html` directamente mediante `file://` para probar la autenticación.

## Publicación en GitHub Pages

1. Crear o seleccionar un repositorio.
2. Subir todo el contenido del paquete a la raíz de la rama `main`.
3. Confirmar que `index.html` se encuentra en la raíz.
4. Abrir **Settings > Pages**.
5. Seleccionar **Deploy from a branch**.
6. Seleccionar la rama `main` y la carpeta `/(root)`.
7. Guardar la configuración.
8. Registrar la URL publicada, con barra final, como Redirect URI de tipo SPA.
9. Configurar los permisos delegados requeridos.
10. Validar primero el modo de prueba y después la autenticación real.

Guía detallada:

[Ver documentación de despliegue](docs/DEPLOYMENT.md)

## Pruebas y evidencias

El repositorio incluye:

- [TEST-REPORT.md](TEST-REPORT.md): resumen legible de las pruebas;
- `tests/static-validation.json`: validaciones estructurales y estáticas;
- `tests/browser-flow-results.json`: flujo automatizado en navegador;
- `tests/sample-download-results.json`: validación del reporte de muestra;
- [docs/TESTING.md](docs/TESTING.md): guía de pruebas posteriores a la publicación.

## Personalización

### Contenido de interfaz

Los textos de la aplicación están localizados en español e inglés. Cualquier modificación debe mantenerse en ambos idiomas y conservar la actualización del atributo `lang` del documento.

### Identidad visual

La aplicación utiliza el estándar de CoE Toolkit:

- Aptos Display para títulos;
- Aptos para el resto de los textos;
- cabecera negra;
- línea multicolor;
- gradiente oscuro corporativo;
- footer estándar;
- favicon oficial;
- controles de versión, autor e idioma.

### Reporte

El reporte PDF debe conservar:

- estructura ejecutiva;
- versión pública;
- pie de página uniforme;
- traducciones completas;
- advertencias de alcance;
- enlaces a herramientas, libros y autor.

### Datos de muestra

Los datos del modo de prueba deben permanecer claramente identificados como ficticios y no deben utilizar nombres, IDs o información sensible de un tenant real.

## Libros relacionados

### Español

- [Definiendo la estructura marco para el Centro de Excelencia de Power Platform](https://www.amazon.com/-/es/Definiendo-estructura-Centro-Excelencia-Platform/dp/B0FSDWQMHW/ref=tmm_pap_swatch_0)
- [Copilot Studio y el futuro del Centro de Excelencia de Power Platform](https://www.amazon.com/-/es/Nicol%C3%A1s-Andr%C3%A9s-Fern%C3%A1ndez/dp/B0GZGL3T1K/ref=tmm_pap_swatch_0)

### English

- [Defining the Framework Structure for the Power Platform Center of Excellence](https://www.amazon.com/-/es/Defining-Framework-Structure-Platform-Excellence/dp/B0GDDRCD2C/ref=tmm_pap_swatch_0)
- [Copilot Studio and the Future of the Power Platform Center of Excellence](https://www.amazon.com/-/es/Nicol%C3%A1s-Andr%C3%A9s-Fern%C3%A1ndez/dp/B0H2VTJZGR/ref=tmm_pap_swatch_0)

## Otras herramientas del CoE Toolkit

### Power Platform Tenant Inventory Explorer

Explora entornos, recursos, configuraciones de gobierno y señales operativas del tenant mediante una SPA modular.

[Open Power Platform Tenant Inventory Explorer](https://nfernandezba.github.io/power-platform-tenant-inventory-explorer/)

### Power Platform & Copilot Studio Environment Strategy - Quick Assessment

Evalúa la definición, cobertura, documentación, comunicación y vigencia de la estrategia de entornos.

[Open Environment Strategy Quick Assessment](https://nfernandezba.github.io/Power-Platform-Copilot-Studio-Environment-Assessment/)

## Autor

**Nico Fernandez**  
[LinkedIn](https://www.linkedin.com/in/nfernandezba)

## Marcas registradas

Microsoft, Microsoft Power Platform, Power Apps, Power Automate, Power BI, Microsoft Copilot Studio, Microsoft Entra, GitHub, GitHub Pages y otros nombres de productos son marcas registradas o marcas comerciales de sus respectivos propietarios.

Este proyecto es una iniciativa comunitaria independiente y no implica respaldo, certificación o soporte oficial por parte de Microsoft o GitHub.

## Disclaimer

La información presentada depende de los datos devueltos por las APIs de Microsoft, de los permisos del usuario autenticado y de la disponibilidad del servicio.

Los indicadores derivados, incluidos capacidad disponible, capacidad sin asignar, porcentajes y consolidaciones, se calculan a partir de los valores recibidos. Deben validarse contra los portales, contratos y registros oficiales antes de tomar decisiones financieras, contractuales o de licenciamiento.

El software se proporciona bajo los términos de la licencia incluida en el repositorio y sin garantías adicionales.

---

# English

## Overview

**Copilot Studio Credits Monitor** is a read-only web application for reviewing Microsoft Copilot Studio capacity, current environment allocations, and tenant agent inventory.

The solution runs as a static SPA hosted on GitHub Pages. Authentication is performed through Microsoft Entra ID and MSAL with delegated permissions. It requires no backend, database, application secret, scheduled process, or additional infrastructure.

It is intended for:

- Power Platform administrators;
- Copilot Studio administrators;
- Center of Excellence leaders and members;
- solution architects;
- licensing and capacity stakeholders;
- governance and operations teams;
- financial monitoring and adoption stakeholders.

The tool consolidates current information from publicly documented and supported Microsoft APIs. It does not attempt to attribute consumption to individual agents or use undocumented mechanisms to obtain additional data.

## Objective

The primary objective is to help an organisation answer questions such as:

> How much Copilot Studio capacity has the tenant purchased, how much has been allocated, how much has been consumed, and how are current allocations distributed across environments?

It also helps answer:

- Which capacity types does Microsoft return for the tenant?
- What is the indicative remaining capacity?
- How much capacity remains unallocated?
- Which environments have an explicit allocation?
- Which environments have no explicit allocation record?
- How many Copilot Studio agents appear in inventory?
- Which environments contain those agents?
- When was the displayed information last refreshed?

## How it works

The application uses a lightweight flow that runs entirely in the browser.

### Application configuration

On the home screen, the user enters:

- **Application (Client) ID**;
- **Directory (Tenant) ID**.

Both identifiers are public and validated as GUIDs before authentication begins. The redirect URI is calculated dynamically from the published GitHub Pages URL.

The remember option stores only those two public identifiers. It does not store report data.

### Authentication

The application uses Microsoft Entra ID and MSAL with Authorization Code Flow and PKCE.

It does not use:

- a client secret;
- a certificate;
- a managed identity;
- a technical account stored in the repository.

Users can only see information allowed by their assigned roles and permissions.

### Capacity query

The application queries tenant capacity reports and displays:

- purchased capacity;
- allocated capacity;
- consumed capacity;
- indicative available capacity;
- unallocated capacity;
- consumption percentage;
- the last update date reported by Microsoft.

### Capacity types

When Microsoft returns multiple capacity types, users can select:

- an individual type;
- **All capacity types**.

The consolidated option adds the available values and retains a per-type breakdown. Because different types may represent different units, the application displays an interpretation warning and never hides the original values.

### Environment allocations

For each environment, the application attempts to retrieve the current capacity allocation.

When Microsoft returns `404 Not Found` for an environment without an explicit allocation record, the application interprets it as an available allocation of `0` rather than blocking the entire report.

Real authentication, permission, network, and service errors remain visible for troubleshooting.

### Environment and agent inventory

The application retrieves:

- Power Platform environment inventory;
- Copilot Studio agent inventory;
- agent-to-environment relationships when the API provides the required information.

Inventory is presented for administration and governance. It is not an attribution of credit consumption to each agent.

### Test mode

The home screen provides access to a test mode that does not require authentication.

Test mode:

- uses fictional data;
- does not request tokens;
- does not call Microsoft APIs;
- populates all functional pages;
- supports testing filters, translations, and responsive behaviour;
- supports PDF report generation;
- supports downloading the static sample report.

It can also be opened by adding:

```text
?test=1
```

## Application structure

### 1. Home screen

Includes:

- CoE Toolkit visual identity;
- public version;
- author LinkedIn profile;
- ES/EN language selector;
- Client ID and Tenant ID fields;
- calculated redirect URI;
- option to remember public configuration only;
- test-mode entry;
- sample-report download;
- privacy and setup information.

### 2. Summary

Displays:

- primary capacity indicators;
- capacity-type selector;
- per-type breakdown;
- operational signals;
- refresh date and status;
- export and report actions.

### 3. Environments

Displays:

- environment name and identifier;
- type and region when available;
- status;
- allocated capacity;
- percentage of total allocation;
- related agent count;
- filters, search, and CSV export.

### 4. Agents

Displays:

- agent name;
- identifier;
- environment;
- status;
- dates and other metadata when available;
- search, filters, and CSV export.

### 5. About the data

Explains:

- data sources;
- required permissions;
- scope of the information;
- handling of environments without explicit allocation records;
- consolidated-view limitations;
- absence of agent-level consumption;
- privacy and non-persistent behaviour.

## What the user receives

The application provides:

- a current administrative tenant view;
- capacity indicators;
- per-capacity-type breakdown;
- current environment allocations;
- environment inventory;
- agent inventory;
- local CSV exports;
- an executive PDF report;
- a complete test mode;
- a static sample report;
- navigation to other CoE Toolkit tools.

## PDF report

The report is generated locally in the browser and follows the CoE Toolkit executive-report visual standard.

Depending on available data, it includes:

- cover and metadata;
- executive summary;
- report scope;
- capacity indicators;
- operational signals;
- capacity-type breakdown;
- assigned environments;
- agent distribution;
- environment appendix;
- agent appendix;
- data limitations;
- related tools;
- related books;
- author and LinkedIn profile.

The PDF is downloaded directly to the user’s device. The application does not retain a copy.

Sample report:

[Download the sample PDF report](assets/reports/Copilot_Studio_Credits_Monitor_Sample_Report_v1.0.pdf)

## CSV exports

Environment and agent views can be exported as CSV files.

Exports:

- are generated in the browser;
- reflect data and filters available in the current session;
- are not sent to an application server;
- are not stored by the tool.

The application does not provide JSON export of functional data.

## Privacy and data handling

Copilot Studio Credits Monitor has no backend and no application database.

During an authenticated session, the browser communicates directly with:

- Microsoft Entra ID for authentication;
- Microsoft Power Platform API for capacity, environment, allocation, and inventory queries.

Functional data remains in memory and is removed when the page is reloaded, closed, or signed out.

The following may be stored locally on an optional basis:

- Application (Client) ID;
- Directory (Tenant) ID;
- selected language.

The application does not automatically store:

- purchased, allocated, or consumed credits;
- environments;
- agents;
- complete API responses;
- generated reports;
- history;
- snapshots;
- credentials or secrets.

## What the tool does not do

The application does not:

- attribute credit consumption to individual agents;
- retrieve consumption by topic, action, tool, or conversation;
- use internal or undocumented PPAC endpoints;
- scrape the administration portal;
- estimate consumption from transcripts;
- retain history between sessions;
- generate scheduled alerts;
- modify capacity allocations;
- replace official Microsoft records;
- replace financial, licensing, or governance processes.

## Technical architecture

The solution uses:

- compiled HTML, CSS, and JavaScript as a static SPA;
- GitHub Pages hosting;
- Microsoft Entra ID;
- `@azure/msal-browser` authentication;
- Microsoft Power Platform API;
- local PDF generation;
- local CSV generation;
- functional state held in memory only.

Simplified flow:

```text
User
  │
  ▼
GitHub Pages SPA
  │
  ├── Microsoft Entra ID / MSAL
  │
  └── Microsoft Power Platform API
          ├── Tenant capacity
          ├── Environment allocations
          ├── Environments
          └── Agent inventory
```

## Permissions and APIs

The App Registration must be configured as a **Single-page application** and use delegated permissions.

Required permissions:

```text
Licensing.Allocations.Read
EnvironmentManagement.Environments.Read
ResourceQuery.Resources.Read
```

Administrative consent may be required under organisational policy.

The application must not be configured with a client secret because any secret included in a GitHub Pages repository or bundle would be visible to users.

## Repository structure

```text
/
├── index.html
├── README.md
├── LICENSE
├── .nojekyll
├── TEST-REPORT.md
│
├── assets/
│   ├── icons/
│   ├── images/
│   │   ├── books/
│   │   └── tools/
│   ├── reports/
│   ├── *.css
│   └── *.js
│
├── docs/
│   ├── DEPLOYMENT.md
│   └── TESTING.md
│
└── tests/
    ├── static-validation.json
    ├── browser-flow-results.json
    └── sample-download-results.json
```

The deployment package does not include source code, `node_modules`, workflows, temporary files, or build tooling.

## External dependencies

The application communicates with Microsoft services for authentication and data retrieval.

It may also load resources required for visual presentation and report generation, depending on the published bundle configuration.

External links to books, tools, and LinkedIn are opened only when selected by the user.

## Local use

### Open test mode

The static content can be served with any local HTTP server.

Python example:

```bash
python -m http.server 8080
```

Then open:

```text
http://localhost:8080/?test=1
```

### Test local authentication

For real authentication, the local URL must also be registered as a Single-page application redirect URI in Microsoft Entra ID.

Example:

```text
http://localhost:8080/
```

Opening `index.html` directly through `file://` is not recommended for authentication testing.

## GitHub Pages deployment

1. Create or select a repository.
2. Upload the complete package contents to the root of the `main` branch.
3. Confirm that `index.html` is located at repository root.
4. Open **Settings > Pages**.
5. Select **Deploy from a branch**.
6. Select branch `main` and folder `/(root)`.
7. Save the configuration.
8. Register the published URL, including the trailing slash, as a Single-page application redirect URI.
9. Configure the required delegated permissions.
10. Validate test mode first and then validate real authentication.

Detailed guide:

[View deployment documentation](docs/DEPLOYMENT.md)

## Testing and evidence

The repository includes:

- [TEST-REPORT.md](TEST-REPORT.md): human-readable test summary;
- `tests/static-validation.json`: structural and static validation;
- `tests/browser-flow-results.json`: automated browser flow;
- `tests/sample-download-results.json`: sample-report validation;
- [docs/TESTING.md](docs/TESTING.md): post-publication testing guide.

## Customization

### Interface content

Application text is localized in Spanish and English. Any change should be maintained in both languages and preserve the correct update of the document `lang` attribute.

### Visual identity

The application follows the CoE Toolkit standard:

- Aptos Display for headings;
- Aptos for other text;
- black header;
- multicolour brand line;
- corporate dark gradient;
- standard footer;
- official favicon;
- version, author, and language controls.

### Report

The PDF report should preserve:

- executive structure;
- public version;
- consistent footer;
- complete translations;
- scope warnings;
- links to tools, books, and author.

### Sample data

Test-mode data must remain clearly identified as fictional and must not use names, identifiers, or sensitive information from a real tenant.

## Related books

### English

- [Defining the Framework Structure for the Power Platform Center of Excellence](https://www.amazon.com/-/es/Defining-Framework-Structure-Platform-Excellence/dp/B0GDDRCD2C/ref=tmm_pap_swatch_0)
- [Copilot Studio and the Future of the Power Platform Center of Excellence](https://www.amazon.com/-/es/Nicol%C3%A1s-Andr%C3%A9s-Fern%C3%A1ndez/dp/B0H2VTJZGR/ref=tmm_pap_swatch_0)

### Spanish

- [Definiendo la estructura marco para el Centro de Excelencia de Power Platform](https://www.amazon.com/-/es/Definiendo-estructura-Centro-Excelencia-Platform/dp/B0FSDWQMHW/ref=tmm_pap_swatch_0)
- [Copilot Studio y el futuro del Centro de Excelencia de Power Platform](https://www.amazon.com/-/es/Nicol%C3%A1s-Andr%C3%A9s-Fern%C3%A1ndez/dp/B0GZGL3T1K/ref=tmm_pap_swatch_0)

## Other CoE Toolkit tools

### Power Platform Tenant Inventory Explorer

Explore environments, resources, governance settings, and tenant operational signals through a modular SPA.

[Open Power Platform Tenant Inventory Explorer](https://nfernandezba.github.io/power-platform-tenant-inventory-explorer/)

### Power Platform & Copilot Studio Environment Strategy - Quick Assessment

Assess the definition, coverage, documentation, communication, and currency of the environment strategy.

[Open Environment Strategy Quick Assessment](https://nfernandezba.github.io/Power-Platform-Copilot-Studio-Environment-Assessment/)

## Author

**Nico Fernandez**  
[LinkedIn](https://www.linkedin.com/in/nfernandezba)

## Trademarks

Microsoft, Microsoft Power Platform, Power Apps, Power Automate, Power BI, Microsoft Copilot Studio, Microsoft Entra, GitHub, GitHub Pages, and other product names are trademarks or registered trademarks of their respective owners.

This project is an independent community initiative and does not imply official endorsement, certification, or support from Microsoft or GitHub.

## Disclaimer

The information displayed depends on data returned by Microsoft APIs, the authenticated user’s permissions, and service availability.

Derived indicators, including available capacity, unallocated capacity, percentages, and consolidated values, are calculated from the returned data. They should be validated against official portals, agreements, and records before making financial, contractual, or licensing decisions.

The software is provided under the terms of the repository licence and without additional warranties.

---

## Licence

MIT. See [LICENSE](LICENSE).
