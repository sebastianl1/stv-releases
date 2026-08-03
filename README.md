# STV — Releases / Descargas

Repositorio público de distribución de la aplicación **STV** (streaming de
películas, series y anime en Android). Aquí se publican las **APK firmadas**
como *release assets* de GitHub para que cualquier usuario pueda descargarlas
sin necesidad de iniciar sesión.

> Sitio oficial del proyecto: https://stv-phostv.pages.dev (sdoc)

---

## Aplicaciones distribuidas

El proyecto tiene **tres versiones de UI** según la plataforma objetivo, cada
una con su propia APK:

| Variante | Plataforma | Archivo APK | Rama de origen |
|---|---|---|---|
| **STV (teléfono)** | Android / Google Play-friendly | `STV-PhosTv-arm64-v8a.apk` | `main` |
| **STV TV** | Android TV / Google TV | `STV-TV-arm64-v8a.apk` | `tv` |
| STV Web | Navegador (Cloudflare Pages) | No aplica (se sirve desde sdoc) | `web` |

Cada APK usa un **nombre de archivo estable por variante**, de modo que la URL
`/releases/latest/download/<archivo>` apunta siempre a la última versión sin
cambiar enlaces.

## Última versión

- **V2.3C** (build 23) — 3 de agosto de 2026
  - Distribución del APK a través de GitHub Releases.
  - Botón de descarga activado en la web oficial.
  - Mejoras de rendimiento y estabilidad.

## Cómo descargar

El APK se sirve por **dos vías** (el botón de la web usa el mirror, que es la
más confiable en celulares):

- **Mirror (directo, sin redirects)** — recomendado para Android:
  ```
  https://raw.githubusercontent.com/sebastianl1/stv-releases/main/STV-PhosTv-arm64-v8a.apk
  ```
- **GitHub Releases (CDN oficial)**:
  ```
  https://github.com/sebastianl1/stv-releases/releases/latest/download/STV-PhosTv-arm64-v8a.apk
  ```

O desde el botón "Descargar APK" en https://stv-phostv.pages.dev.

> Nota: el mirror (archivo del repo) y el release asset son **el mismo APK**
> firmado. El mirror se commitea en `main` de este repo; el release asset se
> sube como adjunto del tag de versión correspondiente.

## Flujo de publicación (por versión nueva)

1. **App** (`app-movies/stv/`): incrementar `currentBuild` y `currentVersion`
   en `lib/config/constants/app_info.dart` (idéntico a `versionCode`/`versionName`
   en `android/app/build.gradle.kts`).
2. Compilar: `flutter build apk --release --split-per-abi`.
3. Subir el APK como **release asset** de GitHub con un tag nuevo (p. ej. `v2.3C`).
4. **sdoc** (`src/config.ts`): actualizar `apk.url`, `buildNumber`, `version`,
   `sizeMb` y `releaseNotes`. El push regenera `version.json` en Cloudflare
   Pages, que las APK instaladas consultan para forzar la actualización.

## Documentación técnica

- App y arquitectura: `AGENTS.md` en `app-movies/`.
- Flujo de publicación completo: `WORKFLOW.md` y `PUBLICAR_APK.md` en `app-movies/`.
- Web / manifest de versión: `sdoc/`.
