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
