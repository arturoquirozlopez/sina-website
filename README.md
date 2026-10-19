# SINA — Pintura en Polvo

Sitio web institucional de SINA. Página informativa con catálogo de productos, carta de colores y contacto directo por WhatsApp.

## Tecnología

- HTML5 / CSS3 / JavaScript vanilla
- Sin dependencias externas ni frameworks
- Fuentes: Google Fonts (Inter)
- Hosting: Vercel (sitio estático)

## Estructura del proyecto

```
sina-project/
├── index.html          ← Sitio completo (single-file)
├── assets/
│   ├── favicon.svg     ← Ícono del navegador (vectorial)
│   └── favicon.ico     ← Ícono del navegador (compatibilidad)
├── vercel.json         ← Configuración de Vercel
├── README.md           ← Este archivo
└── DEPLOY_ON_VERCEL.md ← Guía de despliegue paso a paso
```

## Configuración antes de publicar

Abrir `index.html` y actualizar la línea:

```js
const WA_NUMBER = '56912345678'; // ← Reemplazar con el número real
```

El número debe incluir código de país, sin `+` ni espacios. Ejemplo: `56912345678`.

Este valor único controla **todos** los botones y formularios de WhatsApp del sitio.

## Contacto

- Email: contacto@gruposina.cl
- Web: gruposina.cl

## Atribución de cotizaciones

Al cargar la página se leen `gclid`, `gbraid`, `wbraid`, `fbclid` y `utm_*` de la URL, más `location.href` y `document.referrer`. La primera visita queda fija en `localStorage` (`sina_attr_v2`) y en la cookie `sina_first_touch` (~90 días); visitas posteriores no la pisan. Si `sina-track.js` ya guardó esos datos en `sina_attr` (`landing_url`, `utm_*`, `gclid`, `fbclid`, `ref`), se reutilizan esas keys.

Al enviar el formulario `#cotizacion` (y el de la portada) el sitio hace `POST` a `https://app.gruposina.cl/api/marketing/track` con `Content-Type: text/plain;charset=UTF-8` y `event_type: quote_form_submit`, incluyendo empresa o nombre, email, teléfono, detalle, `request_id`, `tracking_ref` y la atribución de primera visita. Los clicks de WhatsApp envían `quote_request_whatsapp`. Si el POST falla, la cotización por WhatsApp sigue igual. No se escribe en Supabase ni se usa `/api/leads/webhook`. El `dataLayer` de GTM no cambia.
