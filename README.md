<h2>1. Cuadro Comparativo de los robots Motoman MH6, IRB140 y EPSON T3-401S</h2>
<h2>1) Tabla comparativa (Motoman MH6, ABB IRB140, EPSON T3-401S)</h2>

<table>
  <thead>
    <tr>
      <th>Característica</th>
      <th>Motoman MH6</th>
      <th>ABB IRB 140</th>
      <th>EPSON T3-401S</th>
    </tr>
  </thead>

  <tbody>

    <tr>
      <td><strong>Tipo / Ejes</strong></td>
      <td>6-ejes articulado</td>
      <td>6-ejes articulado</td>
      <td>4-ejes SCARA (T-series)</td>
    </tr>

    <tr>
      <td><strong>Carga máxima</strong></td>
      <td>6 kg (existe versión MH6-10 de 10 kg)</td>
      <td>6 kg; alcance 810 mm</td>
      <td>3 kg; alcance horizontal ~400 mm; Z stroke ≈150 mm; repetibilidad 0.02 mm</td>
    </tr>

    <tr>
      <td><strong>Alcance (aprox.)</strong></td>
      <td>Hasta ~1.4 m (según versión / montaje)</td>
      <td>810 mm</td>
      <td>400 mm brazo / 150 mm eje Z</td>
    </tr>

    <tr>
      <td><strong>DOF (grados de libertad)</strong></td>
      <td>6 DOF</td>
      <td>6 DOF</td>
      <td>4 DOF (θ1, θ2, Z, U)</td>
    </tr>

    <tr>
      <td><strong>Velocidad / Ciclo</strong></td>
      <td>Ejes rápidos, diseño para alta velocidad</td>
      <td>Alta aceleración; ciclos rápidos</td>
      <td>Ciclo típico ~0.54 s (dependiendo trayectoria)</td>
    </tr>

    <tr>
      <td><strong>Precisión / Repetibilidad</strong></td>
      <td>≈0.08 mm (según modelo)</td>
      <td>Alta precisión; repetibilidad según configuración</td>
      <td>≈0.02 mm</td>
    </tr>

    <tr>
      <td><strong>Montaje</strong></td>
      <td>Suelo / pared / invertido</td>
      <td>Suelo / pared / invertido</td>
      <td>Mesa / sobremesa / integrado (All-in-One)</td>
    </tr>

    <tr>
      <td><strong>Aplicaciones típicas</strong></td>
      <td>Ensamblaje, manipulación, dispensado, mecanizado ligero, soldadura ligera</td>
      <td>Soldadura, ensamblaje, machine tending, pulido, manipulación general</td>
      <td>Pick & place, ensamblaje ligero, paletizado pequeño, manipulación precisa</td>
    </tr>

    <tr>
      <td><strong>Controlador / Software</strong></td>
      <td>Yaskawa DX100 / MP series; soporte de programación offline</td>
      <td>ABB IRC5; programación RAPID (RobotStudio)</td>
      <td>Controlador RC700/RC90; software EPSON RC+ 7.0; lenguaje SPEL+; USB/Ethernet</td>
    </tr>

  </tbody>
</table>

<p><em>Nota:</em> Las fichas técnicas oficiales deben incluirse en el repositorio como referencia.</p>


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
