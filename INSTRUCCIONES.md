# TradeUp — aplicación conectada a Supabase

Esta versión ya incluye interfaz para:
- Crear cuenta e iniciar/cerrar sesión con correo y contraseña.
- Guardar perfiles en la base de datos: nombre, @usuario, biografía, foto, habilidades y enlaces sociales.
- Publicar y eliminar habilidades.
- Consultar perfiles y dejar una reseña de 1 a 5 estrellas (una reseña por persona).
- Mostrar perfiles destacados a partir de reseñas recibidas (no se puede autoasignar el distintivo).
- Enviar solicitudes de intercambio.
- Mensajería guardada en base de datos y actualizada en tiempo real.

**Importante:** el ZIP incluye el código listo para configurar, pero no puede conectarse a una base de datos hasta que crees tu propio proyecto Supabase y pegues sus datos públicos de conexión. No contiene un servidor propio.

## 1. Crear el proyecto
1. Entra a https://supabase.com/ y crea un proyecto.
2. En el panel del proyecto, abre **SQL Editor** > **New query**.
3. Copia todo el contenido de `supabase-schema.sql`, pégalo y pulsa **Run**.
4. Abre **Storage** > **New bucket**. Crea un bucket llamado `avatars` y activa **Public bucket**.
5. Abre **Project Settings** > **API** (o **Data API / API Keys**, según la interfaz).
6. Copia la **Project URL** y la clave publicable (`anon` / `publishable`).

## 2. Conectar la app
1. Abre `index.html` con un editor de texto.
2. Busca estas dos líneas cerca del inicio del script:
   `const SUPABASE_URL = "PEGA_AQUI_TU_SUPABASE_URL";`
   `const SUPABASE_ANON_KEY = "PEGA_AQUI_TU_CLAVE_PUBLICABLE";`
3. Reemplaza los textos entre comillas con la URL y la clave **publicable** de TU proyecto.
4. Guarda el archivo.

Nunca pegues en `index.html`, GitHub ni chats la clave `service_role` o una clave secreta. La clave publicable está diseñada para el cliente, y las políticas RLS del SQL limitan qué puede hacer cada usuario.

## 3. Publicar en GitHub Pages
1. Sube `index.html`, `supabase-schema.sql`, `tradeup-logo-full.png` y `tradeup-logo-icon.png` a la raíz del repositorio. Mantén los cuatro archivos juntos.
2. En GitHub abre **Settings** > **Pages**.
3. En **Build and deployment**, elige **Deploy from a branch**, selecciona `main` y `/ (root)`, y guarda.
4. Espera a que GitHub Pages muestre el enlace publicado.

## 4. Ajustes recomendados de Supabase Auth
- En **Authentication** > **URL Configuration**, agrega el dominio de GitHub Pages como Site URL y Redirect URL.
- Para pruebas puedes desactivar la confirmación por correo, pero para usuarios reales es mejor mantenerla y configurar el proveedor de correo.
- Configura límites de autenticación y revisa periódicamente las políticas RLS.

## Sobre las reseñas y los destacados
El distintivo “Destacado” se calcula automáticamente con reseñas guardadas: aparecen perfiles con al menos una reseña y se ordenan por promedio y número de reseñas. No es una verificación de identidad ni una garantía de confianza. En una versión pública conviene exigir un intercambio completado antes de permitir reseñas; este prototipo limita a una reseña por persona, pero no comprueba todavía que exista un intercambio completado.

## Privacidad y seguridad
- Prueba primero con cuentas y datos ficticios.
- No pidas ni publiques teléfonos, domicilios, escuela, contraseñas u otros datos sensibles.
- Los enlaces sociales que agregue cada usuario serán visibles públicamente en su perfil.
- Las fotos se guardan en el bucket público `avatars`; usa solo fotos que quieras mostrar públicamente.
- No uses datos de menores reales sin revisar las reglas de privacidad y contar con supervisión adulta y autorización apropiada.
- Este proyecto es un MVP escolar/experimental, no una plataforma auditada para un lanzamiento comercial.
