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

Al cargar la página se leen `gclid`, `gbraid`, `wbraid`, `fbclid` y `utm_*` de la URL, más `location.href` y `document.referrer`. La primera visita queda fija en `localStorage` (`sina_attr_v2`) y en la cookie `sina_first_touch` (~90 días); visitas posteriores no la pisan. Esos datos se envían en **todos** los eventos (`page_view`, `whatsapp_click`, `quote_form_start`, `quote_form_submit`).

Cada POST a `https://app.gruposina.cl/api/marketing/track` lleva `ref` (`SN-XXXXXX`). Sin `ref` el ERP responde 400 y no guarda nada. El formulario envía `quote_form_submit` (crea el lead si hay empresa o nombre, con gclid, UTMs y `landing_url`). El clic de WhatsApp envía `whatsapp_click` y, además, `quote_request_whatsapp` con empresa `Clic WhatsApp`: sin empresa ese evento responde 500 y no se persiste. El mensaje de WhatsApp incluye `Ref cotización: SN-…`.

## Google Ads

El config base `AW-18301590787` se carga en la página si todavía no hay un script de ese ID. Conversiones vía `gtag`:

| Evento | send_to | Valor |
| --- | --- | --- |
| `cotizacion_enviada` | `AW-18301590787/UeiJCJik2aMdEIO68JZE` | 1 CLP |
| `click_whatsapp` | `AW-18301590787/WOJaCJuk2aMdEIO68JZE` | — |

El sitio es HTML estático y **no lee variables de Vercel**. Estos IDs están en `index.html` como valor por defecto. No hace falta definir en producción:

- `NEXT_PUBLIC_GADS_ID=AW-18301590787`
- `NEXT_PUBLIC_GADS_LABEL_QUOTE=UeiJCJik2aMdEIO68JZE`
- `NEXT_PUBLIC_GADS_LABEL_WHATSAPP=WOJaCJuk2aMdEIO68JZE`

Definirlas en Vercel no cambia el sitio mientras no exista un build que las inyecte. Si el ID o el label quedaran vacíos, la conversión no se dispara.
