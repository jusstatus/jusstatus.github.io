# Status page (UptimeRobot)

Página estática que muestra el estado de tus monitores de UptimeRobot. Sin backend: consume la API pública de UptimeRobot directo desde el navegador.

## Uso local

1. Copiá `config.example.js` a `config.js`.
2. Editá `config.js` y poné tu **Read-Only API Key** (UptimeRobot → My Settings → API Settings).
3. Abrí `index.html` (si tu navegador bloquea el fetch por `file://`, servilo con `npx serve .` o `python -m http.server`).

`config.js` está en `.gitignore`: nunca se sube al repo.

## Publicar en GitHub Pages

La clave **no se commitea**. Se inyecta en el momento del deploy desde un GitHub Secret:

1. En el repo de GitHub: **Settings → Secrets and variables → Actions → New repository secret**.
   - Nombre: `UPTIMEROBOT_API_KEY`
   - Valor: tu Read-Only API Key.
2. **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Hacé push a `main`. El workflow [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) genera `config.js` con la clave del secret solo durante el build, publica el sitio, y la clave nunca queda en el historial de git ni en el código fuente del repo.

La clave sigue siendo visible para quien inspeccione el sitio publicado (es inherente a no tener backend), pero como es **read-only** el peor caso es que alguien consuma tu cuota de requests contra la API, no puede modificar monitores.
