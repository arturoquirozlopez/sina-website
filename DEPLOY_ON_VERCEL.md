# Cómo publicar SINA en Vercel

Guía paso a paso para tener el sitio en vivo en gruposina.cl.

---

## Antes de empezar

Abre `index.html` y busca esta línea cerca del final del archivo:

```js
const WA_NUMBER = '56912345678';
```

Reemplaza `56912345678` con el número real de WhatsApp de SINA (código de país incluido, sin `+` ni espacios). Guarda el archivo.

---

## Paso 1 — Crear repositorio en GitHub

1. Ve a [github.com](https://github.com) e inicia sesión (o crea una cuenta gratuita).
2. Haz clic en **New repository** (botón verde arriba a la derecha).
3. Nombre del repositorio: `sina-web` (o el que prefieras).
4. Visibilidad: **Private** (recomendado).
5. Haz clic en **Create repository**.

---

## Paso 2 — Subir los archivos

### Opción A — Desde el navegador (más fácil)

1. Dentro del repositorio recién creado, haz clic en **uploading an existing file**.
2. Arrastra **todos** los archivos y carpetas del proyecto:
   - `index.html`
   - `assets/` (carpeta completa con `favicon.svg` y `favicon.ico`)
   - `vercel.json`
   - `README.md`
   - `DEPLOY_ON_VERCEL.md`
3. Escribe un mensaje de commit, por ejemplo: `Sitio SINA inicial`.
4. Haz clic en **Commit changes**.

### Opción B — Con Git (si tienes Git instalado)

```bash
cd sina-project
git init
git add .
git commit -m "Sitio SINA inicial"
git remote add origin https://github.com/TU_USUARIO/sina-web.git
git push -u origin main
```

---

## Paso 3 — Conectar GitHub con Vercel

1. Ve a [vercel.com](https://vercel.com) e inicia sesión con tu cuenta de GitHub.
2. Haz clic en **Add New → Project**.
3. En la lista de repositorios, selecciona **sina-web**.
4. Haz clic en **Import**.
5. En la pantalla de configuración:
   - **Framework Preset**: Other
   - **Root Directory**: `.` (dejar vacío)
   - **Build Command**: dejar vacío
   - **Output Directory**: dejar vacío
6. Haz clic en **Deploy**.

Vercel detecta automáticamente que es un sitio estático y lo publica en segundos.

---

## Paso 4 — Primer deploy

Vercel asignará automáticamente una URL temporal del tipo:

```
https://sina-web-xxxx.vercel.app
```

Ábrela para verificar que el sitio se ve correctamente antes de conectar el dominio.

---

## Paso 5 — Conectar gruposina.cl

### En Vercel

1. Dentro de tu proyecto en Vercel, ve a **Settings → Domains**.
2. Escribe `gruposina.cl` y haz clic en **Add**.
3. Vercel te mostrará los registros DNS que debes configurar.

### En tu registrador de dominio (NIC Chile u otro)

Accede al panel de DNS de tu dominio y crea los siguientes registros:

| Tipo  | Nombre | Valor                    |
|-------|--------|--------------------------|
| A     | @      | `76.76.21.21`            |
| CNAME | www    | `cname.vercel-dns.com`   |

> Si tu registrador no permite registro A en el apex (`@`), usa el registro ALIAS o ANAME apuntando a `cname.vercel-dns.com`.

4. Espera entre 5 y 30 minutos para que los DNS propaguen.
5. Vercel detectará el cambio automáticamente y activará HTTPS (certificado SSL gratuito).

### Resultado final

```
https://gruposina.cl       ← sitio principal
https://www.gruposina.cl   ← redirige automáticamente
```

---

## Actualizar el sitio en el futuro

Cada vez que subas cambios a GitHub (repite el Paso 2), Vercel redesplegará el sitio automáticamente en menos de 30 segundos.

---

## Soporte

- Vercel Docs: [vercel.com/docs](https://vercel.com/docs)
- NIC Chile DNS: [nic.cl](https://www.nic.cl)
