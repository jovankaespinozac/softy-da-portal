# Softy Data & Analytics — Portal

Portal estático centralizado para los artefactos HTML del equipo de **Data & Analytics** del cliente Softy.  
Desplegado automáticamente en **GitHub Pages** desde la rama `main`.

---

## URL del portal

```
https://<org-o-user>.github.io/softy-da-portal/
```

---

## Estructura del repositorio

```
softy-da-portal/
├── index.html                          ← Home interactivo (portal principal)
├── README.md                           ← Este archivo
├── assets/
│   ├── css/
│   │   └── portal.css                  ← Estilos compartidos del portal
│   └── js/
│       └── portal.js                   ← Lógica de navegación / tabs
├── artifacts/
│   ├── tables/
│   │   └── seguimiento_tablas.html     ← Seguimiento tablas vs modelos BI
│   ├── lineage/
│   │   └── lineage_viewer.html         ← Linaje de tablas
│   └── [categoria]/
│       └── [nuevo_artefacto].html      ← Placeholder para futuros artefactos
└── .github/
    └── workflows/
        └── deploy.yml                  ← GitHub Actions → GitHub Pages
```

---

## Artefactos disponibles

| Artefacto | Ruta | Descripción |
|---|---|---|
| Seguimiento Tablas | `artifacts/tables/seguimiento_tablas.html` | Vista de seguimiento de tablas vs modelos BI |
| Linaje de Tablas | `artifacts/lineage/lineage_viewer.html` | Visualización interactiva del linaje de tablas |

---

## Cómo agregar un nuevo artefacto

1. **Crea la carpeta de categoría** si no existe:
   ```
   artifacts/<categoria>/
   ```

2. **Copia tu archivo HTML autocontenido** en esa carpeta:
   ```
   artifacts/<categoria>/<nombre_artefacto>.html
   ```
   > El archivo debe ser **autocontenido** — todos los estilos y scripts deben ir inline o referenciados por rutas relativas dentro del repo. No dependencias externas que puedan fallar.

3. **Registra el artefacto en `index.html`**:
   - Agrega una entrada en el array `artifacts` dentro del bloque `<script>` de `index.html`.
   - El portal renderizará automáticamente la card en la sección Home y el tab de navegación correspondiente.

   ```js
   { id: "mi_artefacto", label: "Mi Artefacto", category: "categoria", src: "artifacts/categoria/nombre_artefacto.html", description: "Descripción breve del artefacto." }
   ```

4. **Haz push a `main`** — el workflow de GitHub Actions desplegará los cambios automáticamente en GitHub Pages.

---

## Despliegue

El despliegue es automático a través de `.github/workflows/deploy.yml` cada vez que se hace push a `main`.

Para activar GitHub Pages en el repositorio (solo la primera vez):
1. Ve a **Settings → Pages** en GitHub.
2. En **Source**, selecciona **GitHub Actions**.
3. Guarda. El siguiente push a `main` desplegará el portal.

---

## Stack

- HTML, CSS y JavaScript puro — sin frameworks, sin dependencias de build.
- GitHub Actions + GitHub Pages para CI/CD estático.
