
## 1) Tabla comparativa (Motoman MH6, ABB IRB140, EPSON T3-401S)

A continuación se presenta una tabla comparativa de las especificaciones técnicas de los manipuladores:  EPSON T3-401S, Motoman MH6 y el ABB IRB140.

| **Característica** | **Motoman MH6** | **ABB IRB 140** | **EPSON T3-401S** |
|--------------------|------------------|------------------|--------------------|
| **Tipo / Ejes** | 6-ejes articulado | 6-ejes articulado | 4-ejes SCARA (T-series) |
| **Carga máxima** | 6 kg (MH6 estándar; existe MH6-10 de 10 kg) | 6 kg (IRB 140). Alcance 810 mm (hasta eje 5). | 3 kg (payload), alcance horizontal ~400 mm; eje Z stroke ≈150 mm; repetibilidad 0.02 mm |
| **Alcance (aprox.)** | Hasta ~1.4 m (depende versión / montaje) | 810 mm (documentado IRB140) | 400 mm brazo; Z 150 mm |
| **DOF (grados libertad)** | 6 DOF | 6 DOF | 4 DOF (θ1, θ2, Z, U rotación herramienta) |
| **Velocidad / ciclo** | Ejes rápidos — diseñado para alta velocidad (datos por eje en ficha) | Alta aceleración / ciclos rápidos apto para montajes y machine tending | Ciclo estándar ~0.54 s (depende del ciclo). Max. speed ejes T3 según ficha |
| **Precisión / repetibilidad** | ≈0.08 mm (varía por modelo y configuración) | Alta precisión; repetibilidad depende la configuración del IRB140 | ≈0.02 mm (T3 series) |
| **Montaje** | Suelo / pared / invertido (según restricciones de modelo) | Suelo / pared / invertido (flexible) | Mesa / sobremesa (tabletop) / integrado (modelo All-in-One) |
| **Aplicaciones típicas** | Ensamblaje, manipulación, dispensado, mecanizado ligero, soldadura ligera | Soldadura, ensamblaje, manipulado, machine tending, pulido | Ensamblaje, pick & place, paletizado ligero, piezas pequeñas, integrable con visión |
| **Controlador / Software** | Yaskawa controller (DX100 / MP series); soporte para programación offline | ABB IRC5; programación RAPID (RobotStudio) | Controlador RC700/RC90 con EPSON RC+ 7.0; lenguaje SPEL+; integración USB/Ethernet |

> *Nota:* Las fichas técnicas y manuales oficiales de donde se obtuvo la información se encuentran en la carpeta DOCS

## 2) Configuraciones de Home en EPSON T3-401S
El manipulador EPSON T3-401S utiliza encoders absolutos y relativos simultáneamente para determinar la posición angular de cada articulación.

- El encoder absoluto conserva la posición incluso después de apagar el robot.
- El encoder relativo mide desplazamientos desde un punto de referencia durante la operación.

El sistema define su Home en términos de pulsos del encoder (no en grados ni milímetros), según el manual oficial de EPSON, la posición Home estándar coloca todas las articulaciones del robot en 0 pulsos, lo cual representa la configuración geométrica de referencia establecida por fábrica. Sin embargo, en este laboratorio se definió una disposición de Home alternativa, diferente a la del manual, debido a que el Home original limitaba el rango de movimiento lateral y generaba posiciones menos prácticas para la manipulación de objetos. Con el nuevo Home, el robot obtiene un mayor alcance útil hacia ambos lados, especialmente para tareas que requieren desplazamiento amplio sobre la mesa de trabajo. A continuación se presenta la tabla con las posiciones de cada una de las articulaciones en el Home de fábrica: 

| Articulación | Pulsos de Home | Descripción de la posición |
|--------------|--------------------------|-----------------------------|
| **J1**       | 0                        | Brazo 1 orientado hacia el eje +X del robot |
| **J2**       | 0                        | Brazo 2 alineado con Brazo 1 (colineares) |
| **J3 (Z)**   | 0                        | Eje vertical Z en su punto superior (retraído) |
| **J4 (U)**   | 0                        | Herramienta orientada hacia el extremo del brazo 2 (rotación neutra) |

> Esta es la configuración Home **por defecto de fábrica**, utilizada como referencia interna por el controlador.

### Home alternativo definido en el laboratorio

Durante el laboratorio, se implementó un **Home alternativo** debido a que el Home original limitaba el rango de trabajo lateral del robot. El nuevo Home permitió un rango de desplazamiento mayor y más equilibrado hacia ambos lados, facilitando tareas como la manipulación de bandejas y trayectorias amplias.

Valores del Home alternativo configurado:

- **J1 = 204800 pulsos**  
- **J2 = 0**  
- **J3 = 0**  
- **J4 = 0**

Orden de homing asignado:

- **J1 → Step 2**  
- **J2 → Step 2**  
- **J3 → Step 1**  
- **J4 → Step 2**

Esta disposición redefine la orientación inicial del robot, posicionándolo de manera más centrada y aprovechando mejor el espacio de trabajo, tal como se evidencia en la simulación 3D utilizada durante la práctica.

## 3) Procedimiento detallado para movimientos manuales (Teach Pendant / EPSON RC+)

Este apartado describe cómo operar el robot manualmente, tanto usando el teach pendant como el software EPSON RC+ 7.0 conectado por USB, incluyendo cambio de modos de operación, selección de coordenadas (articulaciones vs cartesiano) y la ejecución de traslaciones y rotaciones en los ejes X, Y, Z.

### 1. Modos de operación y conexión  
El robot puede controlarse de dos formas:
- **Teach Pendant (caja de mando manual):** mediante el selector físico de modo del pendante se puede cambiar entre los modos “TEACH” y “AUTO”. 
- **Software EPSON RC+ 7.0 (en PC):** se conecta al controlador del robot mediante cable USB (o Ethernet). En el software se selecciona [Setup] → [PC to Controller Communications] → “USB No. 1” → Connect.
  Una vez conectado el PC, se puede controlar el robot desde el menú [Jog & Teach] o desde [Tools] → [Command Window].

### 2. Cambio de modo  
- En el teach pendant: girar el interruptor de modo a **TEACH** para habilitar el movimiento manual seguro, o a **AUTO** para ejecución de programas. 
- En EPSON RC+: desde la pestaña [Robot Manager] → [Control Panel], asegurarse de que el estado esté en “Motor On” y el modo en TEACH para jog o en AUTO para ejecución.  
- En modo TEACH, los movimientos se limitan para seguridad; en AUTO el robot podrá ejecutar rutinas programadas.

### 3. Selección de sistema de coordenadas  
- **Joint Mode (modo articulaciones):** se mueve cada articulación del robot individualmente (T1, T2, Z, U) usando las flechas J1+/J1-, J2+/J2-, etc.
<img src="Media/Modo_Jogging.png" alt="Foto_programa_joint" width="50%"> 
  
- **Cartesian/Tool/World Mode (modo cartesiano):** se mueve el efector final en los ejes X, Y, Z o se aplica rotación sobre el eje U o la herramienta. En EPSON RC+ se selecciona la pestaña [Jog & Teach] → desplegable “Mode” → Joint / World / Tool.
<img src="Media/Mover_Local.png" alt="Foto_Epson_jog_local" width="50%">

### 4. Ejecución de traslaciones y rotaciones  
- Traslaciones: en modo cartesiano, pulsar X+, X- para mover en X, Y+, Y- para Y, Z+, Z- para Z.  
- Rotaciones: pulsar U+ / U- (o RU+/RU-) dependiendo de la interfaz para rotación de herramienta o eje U.  
- En modo articulaciones: pulsar J1+, J1- etc. para ajustar cada articulación.  
- Para movimientos más precisos se puede usar “step jog” (distancia fija por pulsación) o “continuous jog” (movimiento continuo mientras se mantiene la tecla). En EPSON RC+ se configura el “Jog Distance” y “Jog Speed”.
- Recomendación: antes de mover transversalmente, elevar el eje Z a una altura de aproximación segura para evitar colisiones.

### 5. Seguridad y comprobaciones  
- Asegúrate de que la **puerta de seguridad** esté cerrada o que el interruptor de liberación de enganche esté desactivado antes de operar en modo AUTO. 
- Verifica que se muestre “Safety” atenuado en la barra de estado del RC+ y que los motores estén activados (“Motor On”). 
- Durante el modo TEACH, el robot opera en potencia reducida; en modo AUTO el sistema reproduce el programa completo a la velocidad seleccionada. 

---

Este procedimiento permite al usuario activar, configurar y mover manualmente el robot EPSON T3-401S de forma segura, tanto usando el teach pendant como el software EPSON RC+ 7.0, y realizar traslaciones y rotaciones de forma controlada.

## Niveles de velocidad para movimientos manuales en EPSON RC+ 7.5.2

El robot EPSON T3-401S permite ajustar la velocidad de movimiento manual (**Jogging**) desde el software **EPSON RC+ 7.5.2** o desde el teach pendant (cuando está disponible). Estos niveles afectan únicamente el modo **TEACH**, donde el desplazamiento está deliberadamente limitado por razones de seguridad.

### 1. Tipos de velocidades disponibles (Jog Speed)
En EPSON RC+ 7.5.2 los movimientos manuales utilizan únicamente **dos niveles de velocidad**:

- **Low** → velocidad baja y controlada, recomendada para ajustes cercanos a objetos, enseñanza precisa de puntos y aproximaciones.
- **High** → velocidad elevada dentro del modo TEACH.  
  No tiene un valor fijo ni un límite preestablecido, sino que permite aproximarse al máximo permitido por el sistema en modo seguro. El software limita automáticamente la velocidad para evitar movimientos bruscos.

> A diferencia de otros controladores, el T3-401S **no incluye nivel Medium** en RC+.

El nivel de velocidad afecta tanto al modo **Joint** (movimiento por articulaciones J1–J4) como al modo **Cartesian / Local / World** (movimientos en X, Y, Z, U).

---

### 2. Power Low vs Power High (no confundir con velocidad)
En la ventana **Control Panel** del RC+ aparecen las opciones:

- **POWER LOW**
- **POWER HIGH**

Estas NO son velocidades, sino **niveles de potencia / torque disponible en los motores** durante el movimiento manual.

- **POWER LOW** → torque reducido; ideal para manipulación segura y configuraciones de rutina.
- **POWER HIGH** → torque completo del robot; necesario para mover articulaciones pesadas o superar inercia en ciertos ángulos.

> Aunque esté en POWER HIGH, la velocidad continúa estando limitada por el nivel **Low/High** de Jog Speed y por las restricciones del modo TEACH.

---

### 3. Cómo cambiar los niveles de velocidad en EPSON RC+ 7.5.2

1. Abrir **EPSON RC+ 7.5.2** y conectarse al robot mediante  
   **Setup → PC to Controller Communications → USB Controller → Connect**.
2. Activar los motores: **Motor ON**.
3. Ingresar a la pestaña:  
   **Jog & Teach**.
4. En el panel “Jogging”, ubicar el campo **Speed**.
5. Seleccionar:
   - **Low**
   - **High**
6. Comenzar a mover el robot con los botones de Jog en:
   - **Joint mode**  
   - **Local / World (cartesiano)**  
   - **Tool mode**

El cambio de velocidad es inmediato y afecta todos los vectores de movimiento.

---

### 4. Cómo verificar el nivel de velocidad actual
El nivel activo se puede identificar fácilmente:

#### **En EPSON RC+ 7.5.2**
- En la ventana **Jog & Teach**, en el menú desplegable **Speed**, se muestra el nivel seleccionado (“Low” o “High”).
- El botón se resalta al ser seleccionado.
- El robot también refleja la velocidad en el indicador de estado superior, mostrando que está en **modo TEACH** y con **Jog Speed** activo.

#### **En el Teach Pendant**
- En robots que cuentan con pendante, aparece el indicador **Jog Speed: Low/High** en pantalla.
- La selección se realiza desde los botones del menú Jog.

---

### 5. Recomendaciones de uso
- **Low**: para enseñar puntos, trabajar cerca de objetos, zonas confinadas y ajustes finos.
- **High**: para desplazamientos amplios cuando hay visibilidad total y espacio libre.
- **POWER LOW**: siempre que se trabaje cerca del robot para mayor seguridad.
- **POWER HIGH**: solo cuando los motores requieren más torque.

---

Los niveles de velocidad permiten controlar el desplazamiento del robot durante la enseñanza, combinando seguridad, precisión y fluidez. En EPSON RC+ 7.5.2 estos niveles son simples (Low/High), lo cual facilita la operación y estandariza el comportamiento del T3-401S en modo TEACH.

