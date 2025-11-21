
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

El sistema define su Home en términos de pulsos del encoder (no en grados ni milímetros), según el manual oficial de EPSON, la posición Home estándar coloca todas las articulaciones del robot en 0 pulsos, lo cual representa la configuración geométrica de referencia establecida por fábrica. Sin embargo, en este laboratorio se definió una disposición de Home alternativa, diferente a la del manual, debido a que el Home original limitaba el rango de movimiento lateral y generaba posiciones menos prácticas para la manipulación de objetos. Con el nuevo Home, el robot obtiene un mayor alcance útil hacia ambos lados, especialmente para tareas que requieren desplazamiento amplio sobre la mesa de trabajo.

## A continuación se presenta la tabla con las posiciones de cada una de las articulaciones en el Home de fábrica: 

| Articulación | Pulsos de Home | Descripción de la posición |
|--------------|--------------------------|-----------------------------|
| **J1**       | 0                        | Brazo 1 orientado hacia el eje +X del robot |
| **J2**       | 0                        | Brazo 2 alineado con Brazo 1 (colineares) |
| **J3 (Z)**   | 0                        | Eje vertical Z en su punto superior (retraído) |
| **J4 (U)**   | 0                        | Herramienta orientada hacia el extremo del brazo 2 (rotación neutra) |
| **J5**       | —                        | No aplica para T3-401S |
| **J6**       | —                        | No aplica para T3-401S |

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

<h2>2. Configuración Home del EPSON T3-401S</h2>
<p>
Se describe la posición Home del manipulador, incluyendo la orientación inicial de las articulaciones 
T1, T2, Z y U, su sentido positivo, la altura de referencia del eje Z y el uso del comando 
<strong>HomeSet</strong>. Esta sección explica la correcta definición y recuperación del punto de referencia.
</p>

<hr>

<h2>3. Procedimiento para realizar movimientos manuales</h2>
<p>Se documenta el proceso de operación manual del robot, incluyendo:</p>
<ul>
  <li>Cambio entre modos TEACH y AUTO</li>
  <li>Modo articular (Joint Mode)</li>
  <li>Modo cartesiano (Cartesian Mode)</li>
  <li>Traslaciones y rotaciones en X, Y, Z y U</li>
  <li>Jog continuo y por incrementos</li>
  <li>Habilitación del robot y activación de motores</li>
</ul>

<hr>

<h2>4. Control de velocidades en movimientos manuales</h2>
<p>
Se explican los niveles de velocidad disponibles, cómo cambiar entre ellos y cómo se indica la 
velocidad activa en el software EPSON RC+ 7.0. También se describen condiciones de seguridad 
que limitan automáticamente la velocidad del robot.
</p>

<hr>

<h2>5. Funcionalidades principales del software EPSON RC+ 7.0</h2>
<p>
El repositorio incluye la descripción del entorno RC+ 7.0: editor SPEL+, simulación en 3D, 
configuración de herramientas, manejo de entradas y salidas, compilación y ejecución de programas, 
y comunicación con el controlador RC90/RC700.
</p>

<hr>

<h2>6. Comparación entre EPSON RC+ 7.0, RoboDK y RobotStudio</h2>
<h3>EPSON RC+ 7.0</h3>
<ul>
  <li>Software oficial Epson</li>
  <li>Total compatibilidad con el T3-401S</li>
  <li>Ideal para pruebas físicas y programación real</li>
</ul>

<h3>RoboDK</h3>
<ul>
  <li>Compatible con múltiples marcas</li>
  <li>Excelente para simulación y prototipado</li>
  <li>Incluye post-procesadores para código de robots</li>
</ul>

<h3>RobotStudio</h3>
<ul>
  <li>Software oficial ABB</li>
  <li>Digital Twin avanzado</li>
  <li>Ideal para programación del IRB140</li>
</ul>
