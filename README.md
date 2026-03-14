# 🏍️ Taller Moto 13 — Landing Page

Landing page de alto rendimiento para **Taller Moto 13 Centro de Servicios**,  
ubicado en **Avenida 33 #63-49, Belén, Medellín, Antioquia**.

---

## 📁 Estructura del proyecto

```
taller-moto13/
├── index.html          ← Landing page completa (todo en un archivo)
├── README.md           ← Este archivo
└── og-image.jpg        ← (PENDIENTE) Imagen para Open Graph / redes sociales
```

---

## ✅ Checklist antes de publicar

Antes de desplegar, verifica o actualiza estos puntos en `index.html`:

| # | Qué revisar | Dónde (busca en el código) |
|---|-------------|---------------------------|
| 1 | **Horarios reales** del taller | Sección `#horarios` |
| 2 | **Estadísticas del hero** (años, clientes, calificación) | Clase `.hero-stats` |
| 3 | **Marcas de repuestos** que manejas | Sección `#brands` — `.brands-tape` |
| 4 | **Embed de Google Maps** (iframe real) | Sección `#contacto` — `.map-box` |
| 5 | **Testimonial** — reemplaza con uno real de tus clientes | Clase `.testi-card` |
| 6 | **og-image.jpg** — sube una foto del taller (1200×630px) | `<meta property="og:image">` |
| 7 | **URL canónica** — reemplaza `tallermoto13.co` con tu dominio real | `<link rel="canonical">` |
| 8 | **Schema.org geo** — agrega latitud/longitud exactas | Bloque `<script type="application/ld+json">` |

---

## 🗺️ Cómo obtener el embed de Google Maps

1. Ve a [Google Maps](https://maps.google.com) y busca la dirección del taller
2. Haz clic en **Compartir** → **Insertar mapa**
3. Copia el código `<iframe src="...">` que aparece
4. En `index.html`, busca `<!-- MAPA EMBEBIDO -->` y reemplaza el `src=` del iframe existente

---

## 🚀 Despliegue en Netlify (recomendado — gratis)

### Opción A — Drag & Drop (más fácil, sin registro previo de dominio)

1. Ve a [https://app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra la carpeta del proyecto a la zona de drop
3. ¡Listo! Netlify genera una URL pública en segundos (ej: `https://moto13-abc123.netlify.app`)
4. Para dominio personalizado: **Site settings → Domain management → Add custom domain**

### Opción B — Via GitHub (despliegue continuo)

```bash
# 1. Crea un repo en GitHub y sube los archivos
git init
git add .
git commit -m "feat: landing Taller Moto 13"
git remote add origin https://github.com/TU_USUARIO/taller-moto13.git
git push -u origin main

# 2. En Netlify:
# New site → Import from Git → GitHub → selecciona el repo
# Build command: (dejar vacío)
# Publish directory: . (punto)
# Deploy site
```

### Headers de seguridad en Netlify

Crea un archivo `netlify.toml` en la raíz del proyecto con este contenido para activar los headers de seguridad en el servidor:

```toml
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Permissions-Policy = "camera=(), microphone=(), geolocation=()"
    Content-Security-Policy = "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data: https:; frame-src https://www.google.com; connect-src 'self';"
    Strict-Transport-Security = "max-age=31536000; includeSubDomains; preload"
```

---

## 🚀 Despliegue en Vercel

```bash
# Instala Vercel CLI
npm install -g vercel

# En la carpeta del proyecto
vercel

# Sigue el asistente:
# ¿Link a existing project? → N
# Nombre del proyecto: taller-moto13
# Root directory: ./
# ¡Listo! Vercel genera la URL automáticamente
```

Para dominio personalizado: **Vercel Dashboard → Project → Settings → Domains → Add**

### Headers de seguridad en Vercel

Crea `vercel.json` en la raíz:

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Frame-Options",           "value": "DENY" },
        { "key": "X-Content-Type-Options",    "value": "nosniff" },
        { "key": "Referrer-Policy",           "value": "strict-origin-when-cross-origin" },
        { "key": "Permissions-Policy",        "value": "camera=(), microphone=(), geolocation=()" },
        { "key": "Strict-Transport-Security", "value": "max-age=31536000; includeSubDomains; preload" },
        { "key": "Content-Security-Policy",   "value": "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data: https:; frame-src https://www.google.com; connect-src 'self';" }
      ]
    }
  ]
}
```

---

## 🔒 Seguridad implementada

| Capa | Técnica |
|------|---------|
| XSS prevention | Sanitizador de caracteres en formulario (JS) |
| SQL Injection | No aplica (sin backend); formulario redirige a WhatsApp |
| Spam bots | Honeypot field oculto para humanos |
| Rate limiting | Máximo 3 envíos por 60 segundos (cliente) |
| Clickjacking | `X-Frame-Options: DENY` (meta + headers servidor) |
| Sniffing | `X-Content-Type-Options: nosniff` |
| Data leakage | `Referrer-Policy: strict-origin-when-cross-origin` |
| Permissions | `Permissions-Policy` sin acceso a cámara/micrófono/geo |
| External links | Todos usan `rel="noopener noreferrer"` |
| CSP | Content Security Policy en `netlify.toml` / `vercel.json` |

---

## 🔍 SEO implementado

- ✅ Meta title + description optimizados para Medellín
- ✅ Open Graph (Facebook/WhatsApp preview)
- ✅ Twitter Card
- ✅ JSON-LD Schema.org: `AutoRepair` + 4 `Service`
- ✅ Estructura H1 → H2 → H3 → H4 semántica
- ✅ `alt` implícito en emojis con `aria-hidden`
- ✅ `aria-label` en todos los enlaces importantes
- ✅ `loading="lazy"` en el iframe del mapa
- ✅ `rel="canonical"` configurado
- ✅ `lang="es"` en `<html>`
- ✅ URL de Google Maps en Schema.org `hasMap`

---

## 📞 Datos del negocio

| Campo | Valor |
|-------|-------|
| Nombre | Taller Moto 13 Centro de Servicios |
| Dirección | Avenida 33 #63-49, Belén, Medellín, Antioquia |
| WhatsApp | +57 320 667 2452 |
| Instagram | [@tallermoto13](https://www.instagram.com/tallermoto13) |
| Google Maps | [Ver ubicación](https://maps.app.goo.gl/bRP77WXJYyiJNfrX9) |

---

*Landing page generada con HTML5 + CSS3 + JavaScript vanilla. Sin dependencias de npm. Abre directamente en cualquier navegador.*
