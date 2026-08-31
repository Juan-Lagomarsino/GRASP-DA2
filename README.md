# GRASP — Presentación en Slidev

Presentación compacta (~15–20 min) de los 9 patrones GRASP, dividida para
**6 integrantes**. Resumen de la presentación original de la cátedra
(*Diseño de Aplicaciones 1*).

## Contenido

| Archivo | Qué es |
|---------|--------|
| `slides.md` | La presentación Slidev. Incluye el **guion en las notas del orador**. |
| `GUION.md` | Guion completo por integrante, con tiempos y reparto de diapositivas. |
| `public/` | Diagramas UML en PNG (generados con PlantUML). |
| `diagrams/` | Fuentes `.puml` de los diagramas (por si quieren editarlos). |
| `package.json` | Dependencias y scripts. |

## Cómo verla

Necesitás Node.js 18+. Desde esta carpeta:

```bash
npm install      # solo la primera vez
npm run dev      # abre la presentación en http://localhost:3030
```

- Navegación: **flechas** ←/→.
- **Modo presentador** (ver el guion + la próxima slide): tecla **`p`**,
  o entrá a `http://localhost:3030/presenter`.
- Vista general de todas las diapositivas: tecla **`o`**.

## Exportar a PDF o PPTX

```bash
npm run export                 # genera slides-export.pdf
npx slidev export --format pptx   # genera un .pptx
```

## Antes de presentar

1. Reemplazá **"Integrante 1 … 6"** por los nombres reales en `slides.md`
   (la portada y cada separador de sección `# N · …`).
2. Ensayen una vez completo y cronometren para entrar en la ventana de 15–20 min.

## Editar los diagramas

Los diagramas siguen notación UML y se generaron con PlantUML. Para regenerarlos
tras editar un `.puml`:

```bash
plantuml -tpng -o ../public diagrams/nombre.puml
```
