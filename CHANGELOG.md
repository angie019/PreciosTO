# Registro de cambios — Tecno Outlet (precios.html)

App en vivo: **https://angie019.github.io/PreciosTO/precios.html**
Repositorio: **https://github.com/angie019/PreciosTO**

---

## 18 de julio 2026

### Sincronización en tiempo real entre dispositivos
- Se conectó la app a **Firebase Realtime Database** (proyecto `preciosto`) para que los productos ya no vivan solo en el navegador de cada teléfono (localStorage), sino en una base de datos central en la nube.
- Cuando la persona con acceso al panel admin hace un cambio desde su teléfono (agregar, editar, borrar producto, marcar pauta, crear marca), el cambio se sube a Firebase y se refleja **al instante** en las pantallas de todos los demás dispositivos, sin recargar la página.
- Se agregó un indicador de estado en el panel admin: 🟢 Cambios en vivo / 🟡 Conectando / 🔴 Sin conexión.
- Si un dispositivo pierde internet, sigue mostrando la última copia guardada localmente hasta reconectar.
- Reglas de seguridad de Firebase configuradas para exponer solo el nodo `productos` (lectura y escritura), no la base de datos completa.
- Verificado en producción: una eliminación de producto hecha desde el panel admin se confirmó reflejada correctamente en la base de datos compartida.
- Commit: `b958d3e`

### Orden alfabético
- Todas las marcas (cuadros del catálogo) y todos los productos dentro de cada marca ahora se muestran en orden alfabético, incluida la sección de Especiales/Ofertas.
- El orden es dinámico: cualquier producto o marca nueva que se agregue desde el panel admin se ordena automáticamente, sin necesidad de mantenimiento manual.
- Commit: `1553488`

### Instalar la app como ícono en el teléfono
- Se agregó soporte para "Agregar a pantalla de inicio" (iOS/Android): `manifest.json` + metaetiquetas `apple-touch-icon`.
- El ícono se generó a partir de `logo inicio.png`, recortando el borde de guía de diseño que traía el archivo original y exportando en los tamaños estándar (32, 180, 192, 512, 1024 px).
- Commit: `ccd4729`

### Paneles/modales arriba en vez de abajo
- Los modales de acceso admin, editar producto y crear marca se movieron de la parte inferior a la parte superior de la pantalla, para que el teclado del iPhone no los tape al escribir.
- Commit: `a7949c5`

### Marca de agua, botón de panel y base de datos
- Transparencia de la marca de agua ajustada: primero al 15%, luego afinada al 6% (más tenue) según feedback.
- Reparado el botón ⚙️ de acceso al panel de control (antes no hacía nada; ahora abre correctamente el login de admin).
- Se agregó a INSTA 360 el producto "360 x5 bundle essential" que faltaba respecto al Excel (sin precio definido aún — nota "Consultar precio").
- Se agregó un sistema de versión de datos (`DATA_VERSION`) para que las actualizaciones del catálogo en el código no se queden "atascadas" detrás de una copia vieja guardada en el navegador (localStorage).
- Commit: `6c42d71`

---

## Estado del catálogo (antes de esta sesión)
- Base de datos comparada contra `PRECIOS 23 ABRIL.xlsx`: coincide con el Excel en las 11 marcas (APPLE, CANON, COMPUTADORES, DJI, GARMIN, GOPRO, INSTA 360, NIKON, OTROS, SIGMA, SONY).
- Se identificó que existían archivos duplicados/desactualizados en la carpeta (`tecno-outlet-app.html`, `precios-actualizado.html`) que no están conectados a GitHub Pages — el archivo real y publicado es **`precios.html`**.

---

## Pendientes / posibles mejoras futuras
- **Seguridad del panel admin**: la contraseña actual es solo un candado visual en el código, no una autenticación real. Si se quiere que *solo* la persona autorizada pueda escribir en la base de datos (y no cualquiera que inspeccione el código), se puede agregar Firebase Authentication (usuario y contraseña reales).
- **Precio pendiente**: "360 x5 bundle essential" (INSTA 360) sigue sin precio definido — actualizar cuando se tenga el dato.
- **Rotar el token de GitHub**: el repositorio tiene un token de acceso personal guardado directamente en la configuración de git; se recomienda rotarlo en algún momento por buenas prácticas de seguridad.
