<h2>1. Comparación técnica de los manipuladores</h2>
<p>
Este repositorio incluye un cuadro comparativo de los manipuladores <strong>Motoman MH6</strong>, 
<strong>ABB IRB140</strong> y <strong>EPSON T3-401S</strong>. Se analizan carga máxima, alcance, 
grados de libertad, velocidades, repetibilidad, aplicaciones industriales y software asociado.
</p>

<hr>

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
