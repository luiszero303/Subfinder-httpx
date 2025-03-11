<h2>📌 Paso 1: Encontrar subdominios con <code>subfinder</code></h2>
<p>Ejecutamos el siguiente comando para encontrar subdominios de <code>onetrust.com</code> y guardarlos en un archivo:</p>
<pre><code>subfinder -d onetrust.com -all -o subdominios.txt</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>subfinder</code>: Herramienta para el descubrimiento de subdominios.</li>
    <li><code>-d onetrust.com</code>: Especifica el dominio objetivo.</li>
    <li><code>-all</code>: Usa todas las fuentes disponibles para maximizar la detección de subdominios.</li>
    <li><code>-o subdominios.txt</code>: Guarda los resultados en un archivo llamado <code>subdominios.txt</code>.</li>
</ul>
<img src="https://github.com/luiszero303/Subfinder-httpx/blob/main/paso%201.png" alt="Ejecución de Subfinder" width="450" height="200">

<h2>📌 Paso 2: Analizar subdominios con <code>httpx</code></h2>
<p>Ahora usamos <code>httpx</code> para analizar los subdominios detectados y extraer información útil como códigos de estado HTTP, títulos y tecnologías usadas.</p>
<pre><code>cat subdominios.txt | httpx -status-code -title -tech-detect -o subdominios_mejorados.txt</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>cat subdominios.txt</code>: Muestra el contenido del archivo <code>subdominios.txt</code>.</li>
    <li><code>|</code>: Pasa la salida del primer comando como entrada al siguiente.</li>
    <li><code>httpx</code>: Herramienta para verificar subdominios activos y extraer información.</li>
    <li><code>-status-code</code>: Muestra el código de estado HTTP.</li>
    <li><code>-title</code>: Extrae el título de la página.</li>
    <li><code>-tech-detect</code>: Detecta tecnologías utilizadas en cada subdominio.</li>
    <li><code>-o subdominios_mejorados.txt</code>: Guarda los resultados en un archivo.</li>
</ul>
<img src="https://github.com/luiszero303/Subfinder-httpx/blob/main/paso2.png" alt="Ejecución de Httpx" width="450" height="200">

<h2>📌 Paso 3: Filtrar solo los subdominios con código de estado 200</h2>
<p>Para enfocarnos en subdominios accesibles con código de estado <code>200</code>, ejecutamos:</p>
<pre><code>httpx -status-code -title -tech-detect -mc 200 -o subdominios_200.txt < subdominios.txt</code></pre>

<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>httpx</code>: Ejecuta la herramienta.</li>
    <li><code>-status-code</code>: Muestra el código de estado HTTP.</li>
    <li><code>-title</code>: Extrae el título de la página.</li>
    <li><code>-tech-detect</code>: Detecta tecnologías utilizadas en el subdominio.</li>
    <li><code>-mc 200</code>: <strong>Filtra solo las respuestas con código HTTP <code>200</code> (OK)</strong>.</li>
    <li><code>-o subdominios_200.txt</code>: Guarda la salida en un archivo.</li>
    <li><code>< subdominios.txt</code>: Toma los subdominios de <code>subdominios.txt</code> como entrada.</li>
</ul>
<img src="https://github.com/luiszero303/Subfinder-httpx/blob/main/paso3.png" alt="Filtrado de subdominios 200" width="450" height="200">

<h2>📌 Paso 4: Consideración de otros códigos de estado</h2>
<p>Si bien el código <code>200</code> es importante, también podemos encontrar vulnerabilidades en otros códigos de estado:</p>
<ul>
    <li><code>302 (Found)</code>: Indica redirecciones, lo que puede ser útil para encontrar <strong>open redirects</strong>.</li>
    <li><code>403 (Forbidden)</code>: Puede significar que hay recursos protegidos que podríamos intentar acceder con técnicas de <strong>bypass de restricciones</strong>.</li>
    <li><code>402 (Payment Required)</code>: Puede indicar endpoints premium o bloqueados, útiles en pruebas de <strong>privilege escalation</strong>.</li>
</ul>

<h2>🎯 Conclusión</h2>
<ul>
    <li>🔹 Usamos <code>subfinder</code> para encontrar subdominios activos.</li>
    <li>🔹 Mejoramos la información con <code>httpx</code>, obteniendo códigos de estado, títulos y tecnologías.</li>
    <li>🔹 Filtramos solo los subdominios con código de estado <code>200</code>, lo que nos ayuda a identificar objetivos accesibles.</li>
    <li>🔹 Consideramos otros códigos como <code>302</code> y <code>402</code>, que pueden indicar vulnerabilidades como <strong>open redirects o endpoints protegidos</strong>.</li>
</ul>
<p>Este proceso es fundamental en la fase de reconocimiento de un pentest, ayudando a identificar activos expuestos y posibles vectores de ataque. 🚀</p>
