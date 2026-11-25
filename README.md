# Merlo Autopartes

Sitio web estático y adaptable, desarrollado con HTML, CSS y JavaScript nativo.

## Desarrollo local

Requiere Node.js 24 o posterior y Python 3 para servir el sitio localmente.

```powershell
npm ci
npm run check
py -m http.server 8000 --directory dist
```

Abrí `http://localhost:8000` en el navegador. `npm run check` valida HTML y CSS, crea `dist/` y verifica los recursos locales.

## Integración y despliegue

- GitHub Actions valida HTML y CSS, construye el sitio y verifica los recursos en cada pull request y push a `staging` o `main`.
- Cloudflare Pages usa la integración GitHub para construir y desplegar el sitio.
- `main` es producción; `staging` y los pull requests pueden usar vistas previas de Cloudflare Pages.
- El sitio generado y publicado está en `dist/`.

### Configuración de Cloudflare Pages

1. Crea el proyecto con **Connect to Git** y selecciona este repositorio.
2. Usa el preset **None**, el comando de compilación `npm ci && npm run check` y el directorio de salida `dist`.
3. Configura `main` como rama de producción y habilita las vistas previas para `staging` y los pull requests.
4. Define `NODE_VERSION` como `24` en las variables de entorno de compilación de Cloudflare.
5. Cuando registres el dominio `.com`, conéctalo desde **Custom domains** en la configuración del proyecto.

Con **Connect to Git** no hacen falta los secretos de Cloudflare en GitHub: Cloudflare construye y publica el sitio directamente desde el repositorio. Más información: [Cloudflare Pages con Git](https://developers.cloudflare.com/pages/configuration/git-integration/) y [vistas previas](https://developers.cloudflare.com/pages/configuration/preview-deployments/).
