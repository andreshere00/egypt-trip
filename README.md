# Egipto 25–31 de marzo

Itinerario interactivo de un viaje de siete días por Egipto (Giza, El Cairo, Alejandría, Saqqara y Dahshur), publicado como página estática en GitHub Pages.

**Web:** https://andreshere00.github.io/egypt-trip/

## Qué incluye

- **Itinerario día a día**, con horarios y notas de cada actividad.
- **Un mapa por día** dibujado en SVG, con autopistas, vías principales, calles históricas, el Nilo y los monumentos numerados en el orden de la ruta.
- **Leyenda y distancias**: kilómetros y tiempo aproximado de cada tramo, con el total del día y una escala.
- **Opciones de transporte, entradas y comida** para cada día, con precios estimados.
- **Alojamiento** con buena relación calidad-precio (Giza y Zamalek/Downtown).
- **Presupuesto** por día y total (entradas, transporte, comida y alojamiento), por persona.
- **Tema claro y oscuro** según el sistema, y diseño adaptado al móvil.

## Estructura

```
.
├── index.html   # toda la web: HTML, CSS y JavaScript en un solo archivo
├── .nojekyll    # evita el procesado con Jekyll en GitHub Pages
├── .gitignore
└── README.md
```

No hay dependencias ni paso de compilación. Las únicas peticiones externas son las fuentes de Google Fonts (Cinzel y Alegreya Sans); sin conexión, el navegador usa fuentes de respaldo.

## Cómo está construida

`index.html` contiene el contenido de cada día como HTML y genera mapas, costes y presupuesto con JavaScript a partir de unos bloques de datos al inicio del `<script>`:

| Bloque | Qué define |
| --- | --- |
| `COST` | Costes por evento de cada día (`act`, `trans`, `food`), en euros por persona. Se asocian por orden de aparición. |
| `EXTRA` | Gastos del día que no pertenecen a un evento (desayunos, cenas, taxis). |
| `LODGE` | Precio de la habitación doble por noche. Se reparte entre dos personas. |
| `FLIGHT` | Precio de los vuelos por persona, ida y vuelta. |
| `OPTS` | Opciones de transporte, entradas, comida y alojamiento de cada día. |
| `P` | Puntos del mapa con longitud y latitud. |
| `ROADS`, `NILE`, `SEA`, `DELTA` | Geografía del mapa (carreteras, río, mar y delta). |
| `MAPS` | Mapa de cada día: encuadre, ruta, etiquetas y modo de transporte. |

Las distancias se calculan con la fórmula de Haversine sobre la ruta, multiplicadas por un factor para aproximar el trazado por carretera. El tiempo supone tráfico normal de El Cairo.

### Editar el itinerario

1. Cambia el texto del evento en la sección del día (`<section class="day" id="...">`).
2. Ajusta su coste en `COST` (el orden del array es el de los eventos).
3. Si cambia una parada, edita su punto en `P` y la ruta del día en `MAPS`.
4. Abre `index.html` en el navegador y comprueba el mapa, la leyenda y el presupuesto.

## Probar en local

Abre `index.html` directamente en el navegador, o sirve la carpeta:

```bash
python3 -m http.server 8000
```

Después visita http://localhost:8000.

## Despliegue

La web se publica desde la rama `main`, carpeta raíz, con GitHub Pages. Cada `git push` a `main` la actualiza en uno o dos minutos.

## Supuestos y límites

- Precios en euros por persona, suponiendo dos viajeros que comparten taxi, coche y habitación. Son estimaciones y conviene confirmarlos en las webs oficiales antes de viajar.
- El presupuesto incluye los vuelos (€256 ida y vuelta por persona) y 6 noches de alojamiento. No incluye compras personales, propinas ni seguro.
- Los mapas son esquemas con trazados aproximados. Sirven para orientarse, no para navegar, y la posición de algunos puntos (por ejemplo la rave o el NMEC) es aproximada.
- Los horarios de museos y yacimientos cambian según la fuente. Revisa las webs oficiales unas semanas antes.
