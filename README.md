# Juego 2D de Supervivencia

Juego 2D tipo arcade hecho con **JavaScript puro y HTML5 Canvas**, sin frameworks ni librerías.
Actualmente tiene movimiento y colisiones; enemigos, puntaje y game over en desarrollo.

> Proyecto personal · Inicio: Septiembre 2026 · Estado: En desarrollo ⚒️

🔗 **[Jugar en vivo](https://damianenriquez680.github.io/minijuego_2d/minijuego_2d)**

---

## Descripción

El objetivo es construir un juego de supervivencia en el que el jugador esquive a enemigos que lo persiguen. El proyecto sirve para practicar los fundamentos del desarrollo de videojuegos en la web: el game loop, la lectura del teclado, el dibujo en Canvas y la detección de colisiones.

---

## Estado del proyecto

- [x] Movimiento del personaje
- [x] Colisiones con obstáculos
- [ ] Enemigos que persiguen al jugador
- [ ] Puntaje / temporizador de supervivencia
- [ ] Pantalla de game over y reinicio
- [ ] Dificultad progresiva

---

## Controles

| Acción | Teclas |
|--------|--------|
| Mover arriba | `↑` o `W` |
| Mover abajo | `↓` o `S` |
| Mover izquierda | `←` o `A` |
| Mover derecha | `→` o `D` |

---

## Instalación rápida

No necesita instalación ni dependencias.

```bash
git clone https://github.com/damianenriquez680/minijuego_2d.git
cd minijuego_2d
# Abre minijuego_2d.html en tu navegador (doble clic)
```

O juégalo directamente en línea con el enlace de arriba.

---

## Estructura

```
├── minijuego_2d.html   # Juego completo: HTML, estilos y lógica en JavaScript
└── README.md
```

---

## Elementos del juego

| Elemento | Descripción |
|----------|-------------|
| Escenario | Canvas de 600 × 400 px con fondo blanco |
| Jugador | Cuadrado azul de 30 px que se mueve a 6 px por cuadro |
| Obstáculo | Cuadrado rojo fijo de 80 × 80 px |

El jugador nace en el centro del escenario y no puede salirse del área del Canvas.

---

## Decisiones técnicas

### Game loop
El juego corre en un ciclo con `requestAnimationFrame` que en cada cuadro ejecuta dos pasos separados: `update()`, que calcula el nuevo estado (posiciones y colisiones), y `draw()`, que solo dibuja ese estado en el Canvas. Separar la lógica del dibujo facilita agregar después enemigos, puntaje y pantallas.

### Lectura del teclado
Se guarda en un objeto qué teclas están presionadas, activándolas con `keydown` y desactivándolas con `keyup`. Así el personaje se mueve de forma continua mientras la tecla esté presionada, y se pueden combinar dos teclas para moverse en diagonal.

### Normalización de la velocidad en diagonal
Si el personaje se moviera 6 px en X y 6 px en Y a la vez, avanzaría unos 8.5 px por cuadro, es decir, más rápido que en línea recta. Para evitarlo, cuando hay movimiento en los dos ejes se multiplica cada componente por `√2 / 2` (≈ 0.707), de modo que la velocidad sea la misma en todas las direcciones.

### Colisiones
- **Detección (AABB):** dos rectángulos se están tocando si se solapan en los dos ejes a la vez. Se usa para el personaje y los obstáculos.
- **Resolución por ejes separados:** el movimiento se aplica primero en X y se resuelve la colisión, y después se aplica en Y y se resuelve de nuevo. Al chocar, el personaje se coloca justo en el borde del obstáculo según la dirección en la que venía. Por eso puede deslizarse a lo largo de una pared al avanzar en diagonal, sin vibrar ni dejar huecos.
- **Límites del escenario:** la posición se restringe con `Math.max` y `Math.min` para que el personaje no salga del área del Canvas.

### Dibujo
El personaje se dibuja con coordenadas redondeadas (`Math.round`) para evitar bordes borrosos por posiciones con decimales.

---

## Buenas prácticas aplicadas

- Lógica (`update`) separada del dibujo (`draw`)
- Estado del teclado en un objeto, sin depender de eventos repetidos
- Velocidad normalizada para que el movimiento sea uniforme en todas las direcciones
- Colisiones resueltas por eje para evitar vibraciones y huecos
- Sin dependencias externas: JavaScript puro

---

## Limitaciones conocidas

- La velocidad se aplica **por cuadro** (6 px por frame), así que en monitores con una tasa de refresco mayor a 60 Hz el personaje se mueve más rápido. Está pendiente hacer el movimiento independiente de la tasa de refresco con el tiempo transcurrido entre cuadros (*delta time*).

---

## Tecnologías

- HTML5 Canvas
- JavaScript (sin frameworks ni librerías)

---

## Autor

**Damian Enriquez** — [github.com/damianenriquez680](https://github.com/damianenriquez680)