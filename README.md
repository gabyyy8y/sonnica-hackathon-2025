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
🔹 2. SonNica · Especies (CPT + Metabox + Shortcode)

Funcionalidad: Crea el tipo de contenido “Especies” con metaboxes y shortcode para mostrarlo en el sitio.

Elemento	Descripción
CPT: sonnica_especie	Contiene información de cada ave (nombre común y científico).
Metaboxes:	Campos personalizados: nombre científico, descripción y URL del sonido.
Shortcode: [sonnica_especies]	Muestra grilla responsive con imagen, nombre y audio de cada especie.
🗄️ Base de datos

Tabla principal: wp_thomasmoresonnica_users

CREATE TABLE IF NOT EXISTS `wp_thomasmoresonnica_users` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `nombre` VARCHAR(100) NOT NULL,
  `correo` VARCHAR(120) DEFAULT NULL,
  `especie` VARCHAR(150) NOT NULL,
  `ubicacion` VARCHAR(150) DEFAULT NULL,
  `latitud` DECIMAL(10,6) DEFAULT NULL,
  `longitud` DECIMAL(10,6) DEFAULT NULL,
  `foto` VARCHAR(255) DEFAULT NULL,
  `logro` VARCHAR(100) DEFAULT NULL,
  `fecha_registro` DATETIME DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

🖥️ Interfaz principal
Página de Inicio

Hero con logo de SonNica y ave nacional (Guardabarranco).

Buscador de especies.

Categorías:

🟢 Especies observadas

📚 Catálogo de aves

🗺️ Catálogo de reservas

📈 Logros

📅 Calendario

🎓 Aprenda con SonNica

🎵 Biblioteca de sonidos

Chat flotante

Botón “Chat” con integración hacia Alas Pinoleras en Poe.com

Posicionado arriba del botón de WhatsApp institucional.

🪶 Logros e Insignias de Aviturismo
Insignia	Descripción
🪶 Primer Avistamiento	Primer registro exitoso
🇳🇮 Ave Nacional	Reporta el Guardabarranco
🌄 Madrugador	Avista antes de las 7:00 a.m.
🦜 Amante de la Variedad	5 especies diferentes
🔍 Explorador	3 ubicaciones distintas
🌴 Especialista Tropical	Quetzal, Tucán y Colibrí
🦅 Fanático de Rapaces	Águila, Gavilán, Halcón
🔐 Seguridad y privacidad

Validación en API REST (register_rest_route + nonce).

Restricciones de acceso a endpoints.

No se versionan configuraciones sensibles (wp-config.php, .env, uploads/).

Control de errores y logs (wp_debug.log).

🧠 Tecnologías utilizadas
Categoría	Herramienta
CMS	WordPress 6.x
Lenguajes	PHP 8.2, HTML5, CSS3, JavaScript
Base de Datos	MySQL (phpMyAdmin)
Control de versiones	Git + GitHub
Hosting	unithomasmore.edu.ni
Diseño UI	Figma + CSS Grid + Variables
📂 Estructura del repositorio
sonnica-hackathon-2025/
├─ plugins/
│  ├─ sonnica-register-api/
│  └─ sonnica-especies/
├─ docs/
│  ├─ sql/create_table.sql
│  ├─ endpoints.md
│  ├─ screenshots/
│  └─ schema-db.png
├─ .gitignore
└─ README.md

🚀 Cómo probar localmente

Clonar el repositorio:

git clone https://github.com/gabyyy8y/sonnica-hackathon-2025.git


Copiar los plugins dentro de wp-content/plugins/.

Activar los plugins en el panel de WordPress.

Importar la tabla SQL incluida (docs/sql/create_table.sql).

Probar el endpoint de registro:

POST /wp-json/sonnica/v1/register


Acceder al sitio → https://unithomasmore.edu.ni/sonnica

🧭 Créditos

Estudiantes de Universidad Thomas More
Similly Gabriela Mendoza Barillas
Marcela Alejandra Hernández Molieri 
Tiffany Johanna Coleman González 
Yelitza Paola Sandoval Galeano
Camila de Los Ángeles Mendoza Amador
Proyecto desarrollado por el equipo SonNica – Alas Pinoleras
Integración académica, tecnología y sostenibilidad ambiental 🌱
© 2025 — Todos los derechos reservados.


---

¿Quieres que te prepare también el **`docs/endpoints.md`** y **`docs/sql/create_table.sql`** para que los pegues directo en GitHub y se vea profesional junto con este README?  
Así tu repositorio quedaría completo para mostrarlo al jurado o comité.
