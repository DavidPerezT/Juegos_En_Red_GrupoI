# AAA — Game Design Document

[← Volver al README](README.md)

**Grupo I** · David Perez, David Tardio, Lucia Guzman,Paula Armenteros .

## Índice

1. [Introducción](#1-introducción)
2. [Especificaciones básicas](#2-especificaciones-básicas)
3. [Jugabilidad](#3-jugabilidad)
4. [Narrativa](#4-narrativa)
5. [Imagen y diseño visual](#5-imagen-y-diseño-visual)
6. [Sonido](#6-sonido)
7. [Interfaz y diagrama de flujo](#7-interfaz-y-diagrama-de-flujo)
8. [Comunicación y marketing](#8-comunicación-y-marketing)
9. [Referencias](#9-referencias)

## 1. Introducción

### 1.1. Concepto del juego

Hombre Lobo es un juego de peleas 1 vs 1 para dos jugadores en el que dos jugadores deberan enfrentarse entre ellos . La idea principal
es conseguir un combate estrategico gracias a diferentes elementos como puede ser el posicionamiento , donde cada uno de los personajes
tienen diferentes habilidades y formas de jugar distintas . El objetivo sera bajarle la vida a 0 utilizando los diferentes medios proporcionados.

### 1.2. Propuesta de valor

¿Qué hace diferente a vuestro juego? 

Nuestro juego ofrecera enfrentamientos rapidos y estrategicos , que proporcionara un estilo unico a cada jugador , el protagonista debera aprovechar 
su movilidad y defensa , mientras que el hombre lobo devera aprobechar su gran alcance. Ambos jugadores deberan adaptarse a su rival , aprovechando el escenario 
y eligiendo el momento adecuado.

- Característica diferencial 1: Cada uno de los personajes tendra un estilo unico de juego dando mayor rejugabilidad.
- Característica diferencial 2: Ataques con diferentes areas y efectos.
- Característica diferencial 3: Combates dinamicos y competitivos.

![Imagen promocional / key art del juego](img/portada_presentacion.png)

*Figura 1. Imagen promocional del juego.*


## 2. Especificaciones básicas


| Aspecto | Descripción |
| :--- | :--- |
| **Título** | Hombres Lobo  |
| **Género** | Juego de peleascombate 1 vs 1  |
| **Número de jugadores** | 2 (en red, tiempo real) |
| **Público objetivo** | Jugadores jovenes y adultos que disfrutan de los juegos competitivos y de combate |
| **Clasificación PEGI** | PEGI 16  ya que no se vera contenido explicito pero puede haber sagre y habra combates |
| **Plataforma** | Navegador web (PC), desarrollado con Phaser 3 |
| **Duración de una partida** | 5 min.
| **Representación** | 2D |
| **Licencia** | Apache 2.0 |



## 3. Jugabilidad

### 3.1. Objetivo del juego

El objetivo de cada jugador es reducir a 0 puntos de vida al personaje controlado por el jugador contrario. Un jugador
controla al protagonista, que es pequeño y escurridizo, y el otro controla al hombre lobo, que es más grande y estático.
La partida termina cuando alguno de los dos personajes llega a 0 puntos de vida, y gana el jugador cuyo personaje permanezca con vida.

### 3.2. Controles


| Acción | Jugador 1 | Jugador 2 |
| :--- | :---: | :---: |
| Moverse a la izquierda | `A` | `←` |
| Moverse a la derecha | `D` | `→` |
| Saltar | `W` | `↑` |
| Acción especial AAA | `Espacio` | `Enter` |
| Apuntar / disparar | Ratón (clic izquierdo) | Ratón (clic izquierdo) |
| Pausa | `Esc` | `Esc` |

### 3.3. Mecánicas


#### 3.3.1. Mecánicas principales

- **Movimiento.:**
- El protagonista podrá moverse de forma lineal en cualquier dirección (exceptuando en diagonales). El personaje se moverá
- a un ritmo relativamente lento, para incentivar el uso de la acción de defender. 
-
- **Ataque.:**
El protagonista podrá atacar desde cualquier punto si no está realizando otro ataque o una defensa en el instante en el que el 
jugador presione el botón. Esto ejecutará una animación que impedirá al jugador realizar cualquier otra acción, incluyendo moverse.

La animación tendrá una duración notable que pueda llegar a dejar vulnerable al personaje. Dicha animación debería tener poco start-up 
(tiempo entre que la animación se ejecuta y ataca)  pero tener más end-lag (tiempo entre que se hace el ataque y se vuelve a recuperar el control del jugador),
para que se puedan dar casos en el que el jugador da el golpe de gracia justo antes de recibir un ataque mortal.

El daño a realizar será fijo siempre, sin elementos aleatorios en el daño del ataque. 

- **Defender.:**
El protagonista podrá defenderse en cualquier momento si no está realizando otra defensa o un ataque en el instante en el que el jugador presione el
botón. Esto tendrá una animación que, al igual que al atacar, impedirá al jugador realizar cualquier acción. Dicha animación tendrá más start-up, pero muy poco end-lag.

Tras el start-up de la animación, el protagonista se quedará defendiendo durante el tiempo que el jugador mantenga presionado el botón de defensa. Una vez se suelte,
y haya ese periodo corto de end-lag, el jugador recuperará el control.

Si el jugador recibe un ataque durante este estado, reducirá en un 50% el daño recibido de ese ataque (aunque podría ser una cantidad distinta para prevenir técnicas degenerativas 
de juego, como defenderse, atacar al instante, y defenderse al instante).

Idealmente, durante los primeros instantes de la animación, harías un parry (contraataque)  que evita el 100% del daño y hace un poco de daño al enemigo. Sin embargo esto sería algo
difícil de realizar a nivel técnico.


 **Zarpazos:** 
 El hombre lobo podrá hace zarpazos que ocupan una gran parte del espacio jugable. Sin embargo, sólo podrá hacer un zarpazo a la vez. El jugador tendrá la opción de hacerlo 
 a la izquierda o a la derecha. Estará siempre telegrafiado. 

** Agarre:**
El agarre es otro ataque en área con dos áreas distintas de efecto, siendo casi dos ataques distintos en función de qué tan lejos está el protagonista.

En una distancia corta, el agarre actúa como un ataque en área que ignora la defensa del protagonista. Causa una cantidad definida de daño independientemente de si el protagonista está defendiendo o no.
En una distancia mucho más larga, el agarre causa daño exclusivamente si el protagonista está defendiendo. En caso contrario, no causará daño.

En cualquier caso, la animación debe tener una cantidad considerable de end-lag, para evitar abusar de dicho ataque, y así ser vulnerable ante el protagonista en caso de fallar, y un start-up que de el
tiempo suficiente para que el jugador pueda reaccionar y soltar el botón, pero sólo si tiene muy buenos reflejos.

Es importante evitar espacios huecos en los que el protagonista pueda permanecer sin riesgo.

**Rotación y láser.**

Con los botones de Izq y Der, el sprite del hombre lobo comenzará a rotar sobre sí mismo (sé que no es buena idea rotar sprites, pero es la opción más cómoda). Al pulsar el láser, primero habrá un 
miniláser que aparecerá casi al instante que causará daño, ya que será una penalización por no prestar atención a la rotación del hombre lobo. Tras un poco de tiempo, el láser se ensanchará bastante,
y podrá causar otra instancia de daño. Si, por ejemplo, una persona se queda en el medio del láser y comienza a recibir daño, recibirá 2 puntos de daño. Tras recibirlo, el jugador bloquea, y el láser 
se ensancha, y el jugador recibe 1 punto de daño, en total siendo 3 puntos de daño.

La rotación NO afectará al láser una vez creado.

A la izquierda. el láser rápido. A la derecha, el láser expandido que llega después (el jugador se ha movido y lo esquivó por los pelos).

La rotación NO afecta a ningún otro ataque. La rotación está limitada a rotar hasta que el hombre lobo mire completamente a la izquierda, o a la derecha. 


#### 3.3.2. Objetos y power-ups

El juego no requiere objetos ni power-ups 

#### 3.3.3. Sistema de puntuación

No existe un sistema de puntuación tradicional. La condición de victoria se determina mediante los puntos de vida de ambos personajes. Cada jugador dispone de una cantidad determinada
de puntos de vida al comienzo de la partida y éstos se reducen con cada ataque recibido. El primer jugador cuyo personaje llegue a 0 puntos de vida pierde la partida.

### 3.4. Físicas y dificultad


- **Gravedad y salto:** No hay
- **Colisiones:** Entre jugadores , con los bordes del escenario , obstaculos del escenario .
- **Rebotes / fricción / empujes:** NO hay.
- **Plataformas móviles o superficies especiales (hielo, rebote...):** No hay.
- **Progresión de la dificultad:** a medida que avanza la partida Si el jugador tiene un mayor porcentaje de vida, debería aumentarse el número de obstáculos que aparezcan.
- Si el jugador tiene un menor porcentaje de vida, debería disminuirse el número de obstáculos que aparezcan.
.

### 3.5. Escenario

El escenario representa de forma rectangular pero que no sea algo demasiado ancho. Se pretende que haya algo de verticalidad en juego. Las paredes son sólidas, y el jugador no puede atravesarlos en ningún momento.
. Se compone de la zonas de comabte:

1. **Zona personaje :** Sera por el lado el cual aparezera en personaje para iniciar el juego .
2. **Zona Lobo ** Sera por el lado en el que aparezca el lobo para iniciar el jego .

![Mapa del escenario](img/mapa_escenario.png)

*Figura 2. Mapa del escenario con zonas de aparición, plataformas y obstáculos.*

## Obstáculos para el escenario
Podrán aparecer algunos obstáculos en la sección del protagonista de forma aleatoria. Estos obstáculos serán aproximadamente del tamaño del protagonista. Aparecerán con una pequeña animación de construirse antes 
de que las colisiones del obstáculo se activen. Deben aparecer en lugares aleatorios, pero marcados por una cuadrícula para evitar solapamiento entre los obstáculos.

** Interacción con el protagonista y con el hombre lobo.** 
Con el protagonista, actuarán como paredes inamovibles. El protagonista será incapaz de atravesar estos obstáculos.

El hombre lobo, por su parte, será capaz de destruir todos estos obstáculos con los zarpazos y con el láser. No debería poder destruirlo con el agarre, debido a que haría que todos los obstáculos se destruyan a la
vez debido al área de efecto tan extensa.

** Ratio y límite de aparición de los obstáculos.** 
El ratio de aparición debería ir cambiando, de forma ideal, cuanta más diferencia de porcentaje de vida haya entre el jugador y el hombre lobo. Si el jugador tiene un mayor porcentaje de vida, debería aumentarse el
número de obstáculos que aparezcan. Si el jugador tiene un menor porcentaje de vida, debería disminuirse el número de obstáculos que aparezcan.

En pantalla debería haber siempre un máximo de obstáculos que hayan aparecido. O bien se elimina el obstáculo más antiguo y se spawnea otro en otro lugar, o bien simplemente se espera a que un ataque del hombre lobo rompa 
obstáculos.




## 4. Narrativa

> *Rúbrica — Narrativa:* riqueza de la historia principal y de los personajes.

### 4.1. Historia

AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA.

AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA AAA.

### 4.2. Personajes

#### Protagonista

<img src="img/personaje_1.png" alt="Boceto del personaje AAA" width="250">

- **Edad / origen:** 40 años y su ciudad de origen es de islancia
- **Personalidad:** AAA AAA AAA.
- **Motivación:** AAA AAA AAA.
- **Habilidad especial:** AAA AAA AAA.
- **Trasfondo:** AAA AAA AAA AAA AAA AAA AAA AAA AAA.

#### BBB (Jugador 2)

<img src="img/personaje_2.png" alt="Boceto del personaje BBB" width="250">

- **Edad / origen:** BBB.
- **Personalidad:** BBB BBB BBB.
- **Motivación:** BBB BBB BBB.
- **Habilidad especial:** BBB BBB BBB.
- **Trasfondo:** BBB BBB BBB BBB BBB BBB BBB BBB BBB.

#### CCC (enemigo / personaje no jugable)

<img src="img/enemigo_1.png" alt="Boceto del enemigo CCC" width="250">

CCC CCC CCC CCC CCC CCC CCC CCC.

---

## 5. Imagen y diseño visual

### 5.1. Logotipo

> *Rúbrica — Imagen / Logotipo.*

![Logotipo del juego](img/logo.png)

*Figura 3. Logotipo del juego. Tipografía: AAA. Concepto: AAA AAA AAA.*

### 5.2. Estilo visual

> *Rúbrica — Imagen / Estilo visual:* pixel art, cartoon, vectorial, etc.

El juego utiliza un estilo **AAA** (p. ej. *pixel art* de 32×32 píxeles) porque AAA AAA AAA.

### 5.3. Uso de colores

> *Rúbrica — Imagen / Descripción visual:* uso de colores.

![Paleta de colores](img/paleta_colores.png)

*Figura 4. Paleta de colores del juego.*

- **Fondo (`#1B1F3B`):** AAA AAA AAA.
- **Jugador 1 (`#E94560`) / Jugador 2 (`#0F9BD7`):** colores complementarios para distinguir fácilmente a cada jugador.
- **Objetos (`#F5C518`):** AAA AAA AAA.

### 5.4. Aspectos técnicos: cámara y representación

> *Rúbrica — Imagen / Aspectos técnicos:* uso de cámara y 2D/3D.

- **Representación:** 2D, vista AAA (lateral / cenital / isométrica).
- **Cámara:** AAA (fija mostrando todo el escenario / sigue a ambos jugadores con *zoom* dinámico / pantalla dividida...).
- **Resolución base:** AAA × AAA píxeles.

### 5.5. Inspiración artística y cultural

> *Rúbrica — Imagen / Inspiración:* referentes artísticos y culturales y vínculo con otros trabajos.

![Moodboard de inspiración](img/moodboard_inspiracion.png)

*Figura 5. Moodboard con las referencias visuales.*

- **AAA** (videojuego, año): tomamos AAA AAA AAA [1].
- **BBB** (película / cómic / movimiento artístico): BBB BBB BBB [2].
- **CCC** (referencia cultural): CCC CCC CCC.

### 5.6. Bocetos de personajes y pantallas

> *Rúbrica — Imagen / Bocetos:* interfaz de menú, pantallas y personajes.

Los bocetos de los personajes se encuentran en el apartado [4.2](#42-personajes) y los de las pantallas en el apartado [7.1](#71-pantallas).

---

## 6. Sonido

> *Rúbrica — Sonido:* música y efectos.

### 6.1. Banda sonora

| Pista | Escena | Estilo / ambiente | Fuente / licencia |
| :--- | :--- | :--- | :--- |
| AAA | Menú principal | AAA (p. ej. *chiptune* relajado) | AAA (propia / CC-BY...) |
| BBB | Partida | BBB (p. ej. ritmo rápido, 140 BPM) | BBB |
| CCC | Victoria / derrota | CCC | CCC |

### 6.2. Efectos de sonido

| Efecto | Momento en que se reproduce |
| :--- | :--- |
| Salto | Al pulsar la tecla de salto |
| Golpe / impacto | AAA |
| Recoger objeto | AAA |
| Botones de la interfaz | Al pasar el ratón y al hacer clic |
| Cuenta atrás | AAA |

---

## 7. Interfaz y diagrama de flujo

### 7.1. Pantallas

**Menú principal**

![Boceto del menú principal](img/boceto_menu_principal.png)

*Figura 6. Menú principal: AAA AAA AAA.*

**Pantalla de juego (HUD)**

![Boceto de la pantalla de juego](img/boceto_pantalla_juego.png)

*Figura 7. Pantalla de juego: AAA AAA AAA.*

**Ajustes y fin de partida**

<p align="center">
  <img src="img/boceto_ajustes.png" alt="Boceto de ajustes" width="45%">
  <img src="img/boceto_fin_partida.png" alt="Boceto de fin de partida" width="45%">
</p>

*Figura 8. Pantalla de ajustes (izquierda) y fin de partida (derecha).*

### 7.2. Diagrama de flujo

> *Rúbrica — Documento / Diagrama de flujo.* Podéis usar Mermaid (GitHub lo renderiza directamente) o una imagen exportada.

**Opción 1 — Mermaid** (se dibuja automáticamente en GitHub):

```mermaid
flowchart TD
    A[Pantalla de carga] --> B[Menú principal]
    B --> C[Jugar]
    B --> D[Ajustes]
    B --> E[Ayuda]
    B --> F[Créditos]
    D --> B
    E --> B
    F --> B
    C --> G[Partida]
    G -->|Esc| H[Pausa]
    H -->|Reanudar| G
    H -->|Salir| B
    G -->|Condición de victoria| I[Fin de partida]
    I -->|Revancha| G
    I -->|Volver| B
```

**Opción 2 — Imagen** exportada desde draw.io, Excalidraw, Figma...:

![Diagrama de flujo del juego](img/diagrama_flujo.png)

*Figura 9. Diagrama de flujo entre pantallas.*

---

## 8. Comunicación y marketing

> *Rúbrica — Comunicación / Marketing.*

- **Público y mensaje clave:** AAA AAA AAA.
- **Canales:** redes sociales (AAA, BBB), itch.io, Newgrounds, Game Jolt...
- **Calendario:** *teaser* en AAA, *devlog* semanal en AAA, lanzamiento en AAA.
- **Material:** tráiler, capturas, GIF de jugabilidad, *press kit*.
- **Eslogan:** «AAA AAA AAA».

---

## 9. Referencias

> *Rúbrica — Documento / Referencias.* Usad un formato consistente (p. ej. APA) y citadlas en el texto con [1], [2]...

[1] AAA, A. (Año). *Título de la obra*. Editorial / Estudio. URL

[2] BBB, B. (Año). *Título del artículo*. Revista, volumen(número), páginas. https://doi.org/AAA

[3] Schell, J. (2019). *The Art of Game Design: A Book of Lenses* (3.ª ed.). CRC Press.

[4] Phaser Studio. (s. f.). *Phaser 3 Documentation*. https://docs.phaser.io

[5] Recursos de terceros utilizados (sprites, música, fuentes): AAA — autor — licencia — URL.

sexoooooo