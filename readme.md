# 📋 Reporte de Actividad y Análisis del Sistema GEDOC

**Fecha de reporte:** 10 de julio de 2025  
**Desarrollador:** Damian Muñiz  
**Aplicación:** GEDOC – Gestor de Descargas por SFTP  
**Versión actual:** `v1.1.5`

---

## ✅ Resumen General

La aplicación GEDOC ha sido diseñada para permitir la autenticación de usuarios y la descarga masiva de archivos desde un servidor SFTP. Está dividida en dos módulos principales:

- **Login seguro y gestión de versiones**
- **Interfaz de descarga masiva de archivos vía SFTP**

---

## 🔐 1. Seguridad de la Aplicación

| Elemento                  | Estado Actual                                      |
|--------------------------|----------------------------------------------------|
| 🔑 Autenticación          | Se utiliza `bcrypt` para validar credenciales     |
| 🔒 Variables sensibles    | Almacenadas en `.env` (usuario, contraseña, hash) |
| 🧪 Validación de entradas | Control de intentos e inhabilitación temporal     |
| 🧬 Hash persistente       | Evita regenerar el hash cada ejecución            |
| 🔄 Actualización segura   | Reemplazo automático de `.exe` mediante `.bat`    |
| 🧤 Protección adicional   | Sugerida implementación de PyArmor (pendiente)    |

---

## 📡 2. Conexión a Servidor de Almacenamiento

| Elemento                     | Descripción                                                                          |
|-----------------------------|--------------------------------------------------------------------------------------|
| 🔗 Protocolo de conexión     | `SFTP` mediante `paramiko`                                                           |
| 🔐 Autenticación remota     | Usuario y contraseña extraídos de `.env`                                            |
| 📁 Navegación remota         | Permite explorar carpetas y seleccionar múltiples archivos para descarga            |
| 🗂️ Filtro de búsqueda        | Filtro en tiempo real por nombre de archivo                                          |
| 💾 Carpeta de descarga       | Selección manual del destino local                                                  |
| 📉 Indicador de progreso     | Barra de progreso por archivo                                                       |

---

## 🧪 3. Pruebas Unitarias y Funcionales

| Prueba                                   | Resultado         |
|-----------------------------------------|-------------------|
| 🧪 Inicio de sesión con credenciales     | ✅ Correcto        |
| 🚫 Bloqueo tras múltiples intentos       | ✅ Correcto        |
| 🔄 Verificación de versión remota        | ✅ Funciona        |
| ⚠️ Descarga de nueva versión             | ✅ Se descarga     |
| 🧹 Reemplazo de `.exe` con `.bat`        | ⚠️ Parcial (ver nota) |
| 📁 Listado y navegación de archivos SFTP | ✅ Funciona        |
| 📦 Descarga por lotes                    | ✅ Funciona        |

> **Nota:** El reemplazo del `.exe` a veces falla si el proceso original sigue abierto o si hay permisos de administrador requeridos.

---

## 🛠️ 4. Mejoras Solicitadas y Aplicadas

| Mejora                                               | Estado     |
|------------------------------------------------------|------------|
| 💄 Mejora de interfaz de login con diseño moderno    | ✅ Aplicada |
| 🔐 Mover hash y credenciales a `.env`                | ✅ Aplicada |
| 🔄 Sistema de actualización silenciosa automática    | ✅ Aplicada |
| 🗑 Eliminar `login.exe` anterior tras actualización   | ⚠️ Parcial |
| 📦 Empaquetado como `.exe` único con icono incluido  | ✅ Aplicada |
| 🛡 Protección con PyArmor                            | 🚧 Pendiente |
| 💬 Mostrar versión dinámica en interfaz              | ✅ Aplicada |

---

## 🚀 5. Liberación a Producción

| Fase                       | Detalle                                          |
|---------------------------|--------------------------------------------------|
| 📤 Publicación             | GitHub Releases (`v1.1.5`)                       |
| 🧪 Verificación funcional  | Probado en Windows 10 y 11                       |
| 🧬 Archivos en release     | `login.exe`, `.env`, `assets/icon.ico`          |
| 📌 Instalador              | No requerido, es `.exe` standalone               |
| 📋 Documentación interna   | Agregada en comentarios del código fuente        |
| 🔄 Proceso de actualización | Automático al detectar versión nueva en GitHub |

---

## 🔚 Conclusión

El sistema *GEDOC* cumple con los objetivos funcionales y de seguridad definidos, facilitando la descarga segura de archivos desde un servidor remoto. La app es estable, modular y extensible. Se recomienda:

- Implementar **PyArmor** o método equivalente para ofuscación y protección del `.exe`.
- Considerar añadir **pruebas automatizadas** con `unittest` o `pytest`.
- Evaluar opción de migrar a **instalador con UAC** para mejorar el reemplazo del `.exe`.

---


