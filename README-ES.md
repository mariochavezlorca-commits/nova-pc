# NOVA PC — Manual completo para principiantes

**Frase de marca:** Haz que tu PC se vea legendaria · Tu PC. Tus reglas.

Este proyecto es una página web estática (React + Vite) lista para desplegar en **Vercel**.  
Los visitantes pueden explorar fondos gamer, previsualizarlos y descargarlos. También ven productos recomendados con enlaces de afiliado a Temu.

**Importante:** Esta web **NO cambia el fondo de Windows automáticamente**. Solo descarga el PNG. El usuario debe aplicarlo manualmente en Configuración → Personalización → Fondo.

---

## 1. Cómo empezar (local)

1. Instala Node.js 18 o superior (https://nodejs.org).
2. Abre una terminal en la carpeta del proyecto (donde está `package.json`).
3. Ejecuta:
   ```bash
   npm install
   npm run dev
   ```
4. Abre el enlace que aparece (normalmente http://localhost:5173).

Para generar la versión de producción:
```bash
npm run build
npm run preview
```
La carpeta `dist/` es la que Vercel publica. **Nunca edites archivos dentro de dist/**; edita `src/` y `public/` y vuelve a compilar.

---

## 2. Estructura del proyecto (qué archivo editar)

| Quiero cambiar... | Archivo |
|-------------------|---------|
| Colores, tipografía, tamaños, responsive, animaciones | `src/style.css` |
| Textos, secciones, botones, lógica de la interfaz | `src/main.jsx` |
| Fondos (nombres, descripciones, archivos) | `src/data/themes.js` |
| Productos, precios, enlaces Temu, campañas, TikTok | `src/data/products.js` |
| Fotos de productos | `public/products/` |
| Fondos PNG | `public/wallpapers/` |
| Logo, banner de inspiración | `public/images/` |
| Aviso de privacidad | `public/legal/privacidad.html` |
| Términos | `public/legal/terminos.html` |
| Cookies / almacenamiento | `public/legal/cookies.html` |
| Afiliados / publicidad | `public/legal/afiliados.html` |
| Título, descripción SEO, favicon | `index.html` |
| Cabeceras de seguridad y Vercel | `vercel.json` |
| PWA / offline | `public/manifest.webmanifest`, `public/sw.js` |

---

## 3. Cómo agregar un fondo nuevo

1. Coloca el archivo PNG (recomendado 1920×1080 o superior) en:
   ```
   public/wallpapers/mi-fondo.png
   ```
2. Abre `src/data/themes.js` y agrega un objeto:
   ```js
   {
     id: "mi-fondo",
     name: "NOVA MI ESTILO",
     type: "Categoría / Estilo",
     desc: "Descripción corta del fondo.",
     color: "#35d7f5",
     file: "mi-fondo.png",
     tag: "NUEVO"
   }
   ```
3. Guarda, ejecuta `npm run dev` y comprueba que la imagen carga.
4. La ruta en el navegador será `/wallpapers/mi-fondo.png` (sin escribir `public`).

**Consejo:** Usa nombres en minúsculas sin espacios. Si la imagen no aparece, revisa mayúsculas/minúsculas y la extensión real del archivo.

---

## 4. Cómo agregar un producto

1. Coloca la foto PNG en:
   ```
   public/products/nombre-producto.png
   ```
2. Abre `src/data/products.js` y copia un objeto del arreglo `products`:
   ```js
   {
     id: "mi-producto",
     name: "Nombre del producto — Tipo",
     category: "Mouse",          // o Controles, Audio, etc.
     image: "/products/nombre-producto.png",
     url: "https://temu.to/k/xxxxx",   // o null si aún no tienes enlace
     price: "Precio compartido: MX$xxx (puede cambiar)",  // o null
     description: "Descripción breve y honesta. Confirma detalles en Temu."
   }
   ```
3. Si `url` es `null`, el botón mostrará "Enlace próximamente".
4. Los precios son referencias históricas; siempre indica que pueden cambiar.

---

## 5. Cómo cambiar un enlace Temu

Edita `src/data/products.js`:
- Productos individuales → campo `url` de cada producto.
- Campaña de recompensas → `rewardCampaign.url`
- Invitación de afiliados → `affiliateInvite.url` y `code`

Siempre usa:
```
rel="sponsored nofollow noopener noreferrer"
```
(ya está en el código).

---

## 6. Cómo agregar TikTok

En `src/data/products.js`, dentro de `tiktokLinks`:
```js
export const tiktokLinks = [
  { label: "Setup gamer RGB", url: "https://www.tiktok.com/@tuusuario/video/1234567890" },
];
```
Solo URLs públicas reales de TikTok. Si el arreglo está vacío, la sección no aparece.

---

## 7. Datos legales pendientes (OBLIGATORIO antes de publicar)

Abre `DATOS-LEGALES-PENDIENTES.md` y completa:

- Nombre completo o razón social del responsable
- Domicilio para oír y recibir notificaciones
- Correo de privacidad / ARCO
- Correo de contacto general

Luego sustituye los marcadores `[NOMBRE...]`, `[DOMICILIO...]`, `[CORREO...]` en los cuatro archivos de `public/legal/`.

Los documentos son **borradores informativos**. Recomiéndalos con un profesional antes de publicar comercialmente.

---

## 8. Despliegue en Vercel (paso a paso)

1. Crea una cuenta gratuita en https://vercel.com
2. Sube este proyecto a GitHub (recomendado):
   - Crea un repositorio nuevo
   - Sube todos los archivos **excepto** `node_modules/` y `dist/`
3. En Vercel → **Add New Project** → Importa el repositorio.
4. Configuración:
   - Framework Preset: **Vite**
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Install Command: `npm install`
5. Pulsa **Deploy**.
6. Cuando termine, Vercel te dará una URL (ejemplo: `https://nova-pc.vercel.app`).

Cada vez que hagas cambios:
1. Edita los archivos fuente (`src/` o `public/`)
2. Haz commit y push a GitHub
3. Vercel vuelve a desplegar automáticamente

También puedes usar Vercel CLI:
```bash
npm i -g vercel
vercel
```

---

## 9. Seguridad y privacidad (resumen)

- No se piden datos personales.
- Favoritos y preferencias se guardan solo en el navegador (localStorage).
- Notificaciones: se piden solo después de que el usuario acepte un aviso claro.
- Enlaces de afiliado están identificados como publicidad.
- No hay popups forzados ni redirecciones automáticas a Temu.
- Cabeceras de seguridad configuradas en `vercel.json`.

---

## 10. Limitaciones reales del sitio

- **No modifica Windows.** Solo descarga fondos. El usuario aplica el cambio manualmente.
- No hay backend, cuentas de usuario ni base de datos.
- No hay notificaciones push reales de ofertas (solo prueba local del navegador).
- Los precios y disponibilidad de Temu no se actualizan automáticamente.
- Los enlaces de productos sin `url` muestran “Enlace próximamente”.

---

## 11. Comandos útiles

```bash
npm install          # Instalar dependencias
npm run dev          # Desarrollo local
npm run build        # Compilar para producción
npm run preview      # Previsualizar la carpeta dist
```

Si una imagen no carga:
1. Revisa que el nombre del archivo coincida exactamente (mayúsculas, extensión).
2. La ruta empieza desde `public/` pero en el código se escribe sin `/public` (ejemplo: `/wallpapers/nova-neon.png`).
3. Abre la consola del navegador (F12) y mira errores 404.

---

**Versión:** 1.0.0 (producción lista para Vercel)  
**Fecha de esta guía:** 18 de noviembre de 2026  
**Idioma:** Español de México
