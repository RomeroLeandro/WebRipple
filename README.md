# WebRipple — Landing Oficial

Landing page del emprendimiento WebRipple, construida con Astro.

## 🚀 Cómo arrancar

```bash
# Instalar dependencias
npm install

# Servidor de desarrollo
npm run dev

# Build para producción
npm run build

# Preview del build
npm run preview
```

La app corre en `http://localhost:4321`

---

## 📁 Estructura del proyecto

```
webripple/
├── src/
│   ├── layouts/
│   │   └── Layout.astro        ← HTML base, fuentes, variables CSS
│   ├── components/
│   │   ├── Navbar.astro         ← Navegación fija con menú mobile
│   │   ├── Hero.astro           ← Sección principal con mockup
│   │   ├── Services.astro       ← Cards de servicios
│   │   ├── Portfolio.astro      ← Trabajos realizados
│   │   ├── Pricing.astro        ← Planes con Mercado Pago
│   │   └── ContactFooter.astro  ← Contacto + Footer
│   └── pages/
│       └── index.astro          ← Página principal
├── public/                      ← Assets estáticos (logo, imágenes)
├── astro.config.mjs
└── package.json
```

---

## 💳 Configurar Mercado Pago

### Paso 1 — Crear cuenta y app
1. Entrá a https://www.mercadopago.com.ar/developers
2. Creá una aplicación nueva
3. Copiá tu **Public Key** y **Access Token**

### Paso 2 — Crear preferencias de pago

Usá la API de Mercado Pago para generar los `preference_id` de cada plan:

```bash
curl -X POST \
  'https://api.mercadopago.com/checkout/preferences' \
  -H 'Authorization: Bearer TU_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
    "items": [{
      "title": "Landing Page Starter - WebRipple",
      "quantity": 1,
      "currency_id": "ARS",
      "unit_price": 80000
    }],
    "back_urls": {
      "success": "https://webripple.com.ar/gracias",
      "failure": "https://webripple.com.ar/error",
      "pending": "https://webripple.com.ar/pendiente"
    },
    "auto_return": "approved"
  }'
```

La respuesta incluye el `id` que va en el link del botón de pago.

### Paso 3 — Actualizar links en Pricing.astro

En `src/components/Pricing.astro`, reemplazá:
```
TU_PREFERENCE_ID_STARTER   → el id del plan Starter
TU_PREFERENCE_ID_PRO       → el id del plan Pro
TU_PREFERENCE_ID_ECOMMERCE → el id del plan Ecommerce
```

---

## 🌐 Deploy en Netlify (gratis)

```bash
# Build
npm run build

# La carpeta dist/ es la que se sube a Netlify
# Arrastrá esa carpeta en netlify.com/drop
```

O conectá el repo de GitHub a Netlify para deploy automático.

---

## ✏️ Personalizar

### Cambiar número de WhatsApp
Buscá `5491112345678` en todos los archivos y reemplazalo por tu número.

### Cambiar email
Buscá `hola@webripple.com.ar` y reemplazalo.

### Agregar proyectos al portfolio
Editá el array `works` en `src/components/Portfolio.astro`.

### Cambiar precios
Editá el array `plans` en `src/components/Pricing.astro`.
