# 🐦 SonNica · Alas Pinoleras

**SonNica** es una plataforma web desarrollada en **WordPress + PHP + MySQL**, diseñada para promover la observación y registro de aves en Nicaragua.  
El sistema integra registro de usuarios, catálogo de especies y reservas naturales, logros de aviturismo y un panel interactivo tipo app.

---

## 🌍 Descripción general

El proyecto forma parte del **Hackathon SonNica 2025**.  
Su objetivo es ofrecer una experiencia educativa y ambiental mediante el registro de avistamientos de aves y la exploración de especies y reservas naturales.

### Componentes principales:
- **Registro e inicio de sesión:** Usuarios pueden registrarse o iniciar sesión (autenticación con API personalizada).
- **Nuevo Avistamiento:** Permite registrar una especie observada, subir su foto y ubicación (latitud/longitud).
- **Catálogo de Aves:** Visualización interactiva de especies registradas con imágenes y audios.
- **Catálogo de Reservas:** Mapa de reservas y hotspots de avistamiento.
- **Logros:** Sistema de insignias por número de avistamientos o especies distintas.
- **Biblioteca de Sonidos:** Audios representativos de aves nicaragüenses.
- **Interfaz moderna y responsive:** Adaptada para escritorio y móvil con diseño en HTML + CSS puros.

---

## 🧩 Arquitectura del sistema

**Modelo MVC simplificado dentro de WordPress:**

| Capa | Elemento | Descripción |
|------|-----------|-------------|
| **Model** | `wp_thomasmoresonnica_users` | Tabla que almacena usuarios, especies, coordenadas, fotos y logros. |
| **Controller** | Plugin `SonNica Register API` | Endpoint REST para registrar, autenticar y almacenar datos en la BD. |
| **View** | Plugin `SonNica Especies (CPT + Metabox + Shortcode)` | Renderiza la grilla de especies, reservas y logros. |

---

## ⚙️ Plugins del proyecto

### 🔹 1. SonNica Register API
**Funcionalidad:** Control de usuarios y registro de avistamientos mediante la REST API de WordPress.  
**Rutas principales:**

| Método | Endpoint | Descripción |
|---------|-----------|-------------|
| `POST` | `/wp-json/sonnica/v1/register` | Crea un nuevo usuario + autologin |
| `POST` | `/wp-json/sonnica/v1/login` | Inicia sesión |
| `POST` | `/wp-json/sonnica/v1/guest` | Crea sesión temporal (visitante) |
| `GET`  | `/wp-json/sonnica/v1/ping` | Verifica conexión con el servidor |

**Estructura del registro:**
```json
{
  "nombre": "Jimmy",
  "correo": "jimmy@unithomasmore.edu.ni",
  "especie": "Guardabarranco",
  "ubicacion": "Thomas More",
  "latitud": 12.145678,
  "longitud": -86.271234,
  "foto": "https://unithomasmore.edu.ni/wp-content/uploads/2025/10/guardabarranco.jpg",
  "logro": "Primer Avistamiento"
}
