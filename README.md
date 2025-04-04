# Proyecto de Juego de Plataformas con IA basada en NEAT

> *"La inteligencia artificial no reemplaza la creatividad humana, pero puede amplificarla en formas sorprendentes."* — Desarrollador anónimo

---

##  **Resumen**

Este proyecto **tenía**** como objetivo desarrollar un juego de plataformas interactivo en 2D, donde un jugador compita o colabore con un personaje controlado por una **IA basada en NEAT** (_NeuroEvolution of Augmenting Topologies_).

Durante el desarrollo surgieron desafíos técnicos que produjeron el cambio entre diversas tecnologías:

- Eclipse + Java
- Bibliotecas gráficas como *LibGDX* y *Slick2D*
- Finalmente, el motor **Godot**

Actualmente, el proyecto se encuentra en desarrollo en Python con un prototipo básico funcional y el diseño de la IA en curso.

---

##  **Introducción**

El desarrollo de videojuegos implica tanto *creatividad en el diseño* como capacidad para adaptarse a las limitaciones técnicas. Este proyecto se **basaba** centra en un juego de plataformas 2D donde el jugador interactúa con un NPC controlado por **IA**.

El foco está en la implementación del algoritmo **NEAT**, permitiendo al NPC *aprender y mejorar sus habilidades de forma autónoma*.

> La inclusión de IA representa la fase más compleja y desafiante del proyecto.

---

##  **Objetivos actuales**

1. Establecer una base sólida para un juego funcional.
2. Implementar una IA básica para el NPC.
3. Explorar y ajustar herramientas para futuras iteraciones.

---

##  **Metodología**

###  Fase 1: Configuración inicial con Eclipse y Java

- Uso de **LibGDX** para gráficos 2D.
- Problemas técnicos con la configuración.

###  Fase 2: Transición a Slick2D

- Librería ligera y sencilla.
- Limitaciones gráficas y funcionales.

###  Fase 3: Evaluación de motores gráficos

- **Unity** descartado por su complejidad y licencias.
- **Godot** elegido por ser:
  - Código abierto
  - Fácil de aprender
  - Óptimo para 2D

###  Fase 4: Desarrollo inicial en Godot

- Se construyó un prototipo con:
  - Plataformas estáticas
  - Personaje jugable
  - Mecánicas básicas de movimiento

###  Fase 5: Diseño de la IA

- Implementación del algoritmo **NEAT**
- Uso de *redes neuronales evolutivas*
- Movimientos aleatorios mejorables por evolución

---

##  **Resultados preliminares**

-  Prototipo básico en **Godot**
-  Herramientas definidas para desarrollo
-  IA estructurada para futuras fases

---

##  **Discusión**

> *"No se trata solo de qué herramientas usas, sino de cómo se adaptan a tu proyecto."*

La elección de **Godot** sobre **Unity** fue crucial. Sin embargo, el uso de NEAT sigue representando un gran desafío.

---

##  **Próximos pasos**

-  Integrar completamente el algoritmo NEAT
-  Ampliar el nivel con nuevas mecánicas
-  Evaluar jugabilidad e interacción IA-jugador

---

##  **Agradecimientos**

*Agradezco especialmente a mi amigo*, quien compartió sus apuntes de la asignatura de **IA** de la [Universidad de Sevilla](https://www.us.es/), del **Grado en Ingeniería Informática**.

---

##  Apéndice A: Movimiento del Personaje Jugador

### Código en Godot (GDScript):

```gdscript
extends CharacterBody2D

const SPEED = 130.0
const JUMP_VELOCITY = -300.0

var gravity = ProjectSettings.get_setting("physics/2d/default_gravity")
@onready var animated_sprite = $AnimatedSprite2D

func _physics_process(delta):
    # Gravedad
    if not is_on_floor():
        velocity.y += gravity * delta

    # Salto
    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = JUMP_VELOCITY

    # Dirección
    var direction = Input.get_axis("move_left", "move_right")

    # Animaciones
    if direction > 0:
        animated_sprite.flip_h = false
    elif direction < 0:
        animated_sprite.flip_h = true

    if is_on_floor():
        if direction == 0:
            animated_sprite.play("idle")
        else:
            animated_sprite.play("run")
    else:
        animated_sprite.play("jump")

    # Movimiento
    if direction:
        velocity.x = direction * SPEED
    else:
        velocity.x = move_toward(velocity.x, 0, SPEED)

    move_and_slide()
```
## Explicación del código

### Constantes principales:
- **`SPEED`**: Controla la velocidad horizontal del personaje.  
- **`JUMP_VELOCITY`**: Define la fuerza del salto.

### Uso de gravedad:
La gravedad se sincroniza con la configuración global del proyecto, lo que asegura consistencia con otros nodos físicos.

### Movimiento:
El código captura la dirección del jugador a través de las acciones `move_left` y `move_right`, configuradas en el mapa de entradas del proyecto.

### Animaciones:
El nodo `AnimatedSprite2D` maneja las animaciones del personaje (`idle`, `run`, `jump`).  
El sprite se voltea dependiendo de la dirección del movimiento.

### Física del personaje:
El método `move_and_slide` aplica las velocidades calculadas al nodo `CharacterBody2D`, garantizando que interactúe correctamente con el entorno.
