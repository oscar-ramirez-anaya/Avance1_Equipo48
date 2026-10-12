<div style="text-align: center;">

# Avance 1 | Análisis exploratorio de datos

### EDA de un dataset de planograma para negocios pequeños

**Tecnológico de Monterrey** · Maestría en Inteligencia Artificial Aplicada
**TC5035.10 — Proyecto Integrador (Grupo 10)**

**Equipo 48** · **Modalidad:** En equipo · **Fecha:** Octubre 2026

| Integrante | Matrícula |
|---|---|
| Oscar Alberto Ramírez Anaya | A01795438 |
| Germán Eduardo Rodríguez Vázquez | A01796325 |
| Jesús Soto Medrano | A01794746 |

**Profesora:** Dra. Grettel Barceló Alonso · **Asesor:** Dr. Raúl Valente Ramírez
**Sponsor:** Dr. Juan Arturo Nolazco Flores · **Organización:** Bnext

</div>

---

## Descripción

Análisis exploratorio de datos (EDA) de la fase de *Entendimiento de los datos* de CRISP-ML(Q).
Caracteriza un conjunto de imágenes de anaquel con anotaciones y planograma de referencia: volumen,
resoluciones, clases y espacios vacíos, densidad y tamaño de los objetos, distribución espacial,
estado por posición (correcto, faltante, mal ubicado), métricas de calidad de captura, separabilidad
por color y detección de duplicados.

> **Datos sintéticos.** El EDA se construyó sobre un conjunto **sintético** generado dentro de la
> libreta con semilla fija (`SEED = 48`): 360 imágenes, 12 570 cajas, 8 tiendas con 2 muebles cada una
> y 4 dispositivos de captura. Las cifras ilustran el método de análisis; **no contiene imágenes ni
> datos de Bnext**.

## Contenido

| Archivo | Descripción |
|---|---|
| **`Avance1.48.ipynb`** | Libreta del EDA, ejecutada de principio a fin con salidas y gráficos |
| `Avance1.48.pdf` | Reporte del EDA |
| `Avance1.48.docx` | Reporte en formato editable |
| `POLITICA_DATOS.md` | Acuerdo de manejo de datos con Bnext |

## El notebook — descargar o visualizar

- **Visualizar en GitHub:** [`Avance1.48.ipynb`](./Avance1.48.ipynb)
- **Visor enriquecido (nbviewer):** https://nbviewer.org/github/oscar-ramirez-anaya/Avance1_Equipo48/blob/main/Avance1.48.ipynb
- **Descargar (raw):** https://raw.githubusercontent.com/oscar-ramirez-anaya/Avance1_Equipo48/main/Avance1.48.ipynb

## Secciones del notebook

1. Generación del dataset sintético.
2. Visión general, resolución y formato.
3. Clases y espacios vacíos; densidad y tamaño de cajas; mapas de calor espaciales.
4. Métricas de calidad y banderas de imágenes problemáticas.
5. Anatomía de una imagen (bordes de Canny, nitidez).
6. Separabilidad por color (PCA y clasificador de referencia).
7. Duplicados y riesgo de fuga de información.
8. Estado por posición y cumplimiento del planograma; tablero de factibilidad.

## Resultados principales

- 18.9 % de las posiciones están vacías, la clase más frecuente.
- Estado por posición: 71.4 % correcto, 18.9 % faltante, 9.7 % mal ubicado.
- 37.5 % de las imágenes tienen al menos un problema de calidad; en dispositivos básicos sube a 59.5 %.
  La nitidez, determinada por el dispositivo, es la principal fuente de variación.
- Un clasificador que solo usa color logra 0.97 de exactitud (azar: 0.14), lo que advierte un riesgo de brecha entre datos
  sintéticos y reales.
- Los duplicados obligan a particionar por tienda y mueble (GroupKFold) para evitar fuga.

## Notas de consistencia

El reporte y la libreta se redactaron en paralelo y difieren en algunas cifras; la libreta es la
fuente reproducible.

| Concepto | Reporte | Libreta |
|---|---|---|
| Detección de duplicados | dHash 256 bits, P 1.00 / R 0.40 | aHash 64 bits, P 0.93 / R 0.43 |
| Exactitud del clasificador de color | 0.95 | 0.97 |
| Imágenes con al menos un problema de calidad | 38.9 % | 37.5 % |

## Reproducir

```bash
pip install numpy pandas opencv-python-headless matplotlib seaborn pillow scikit-learn nbconvert ipykernel
jupyter nbconvert --to notebook --execute --inplace Avance1.48.ipynb
```

El dataset sintético se escribe en `~/week3/data` (configurable con `AVANCE1_DATA_DIR`).
