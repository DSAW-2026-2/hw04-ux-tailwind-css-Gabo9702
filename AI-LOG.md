# ¿Como implemento un botón de modo oscuro en una página web?
# Incluyendo los iconos de la luna y el sol

Paso 1: Configurar Tailwind para el modo oscuro
Por defecto, Tailwind detecta el modo oscuro del sistema operativo, pero si queremos controlarlo con un botón, debemos decirle que obedezca a una clase CSS.

Agrega esta configuración en tu <head> dentro del script de Tailwind:

HTML
<script>
    tailwind.config = {
        darkMode: 'class', // ¡Esta línea es la magia!
        theme: {
            extend: {}
        }
    }
</script>
Paso 2: Crear el botón con los iconos (HTML)
Necesitamos un botón que contenga ambos iconos (el sol y la luna) en formato SVG. La lógica visual es simple: si estamos en modo claro, ocultamos el sol y mostramos la luna; si estamos en modo oscuro, ocultamos la luna y mostramos el sol. Usaremos la clase hidden para controlarlos.

Coloca este código donde quieras que aparezca tu botón (usualmente en el <header>):

HTML
<button id="theme-toggle" type="button" class="text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg text-sm p-2.5">
    
    <!-- Icono de Luna (Se muestra en modo claro) -->
    <svg id="theme-toggle-dark-icon" class="hidden w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
        <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path>
    </svg>
    
    <!-- Icono de Sol (Se muestra en modo oscuro) -->
    <svg id="theme-toggle-light-icon" class="hidden w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
        <path d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" fill-rule="evenodd" clip-rule="evenodd"></path>
    </svg>
    
</button>
Paso 3: La lógica de JavaScript
Finalmente, el "cerebro" de la operación. Este script hace dos cosas vitales:

Al cargar la página, revisa si el usuario ya tenía el modo oscuro guardado en el navegador (localStorage) para mantenerlo activo.

Escucha los clics en el botón para inyectar o quitar la clase dark de la etiqueta <html>, intercambiar los iconos, y guardar la nueva preferencia.

Pega este bloque justo antes de cerrar tu etiqueta </body>:

HTML
<script>
    // 1. Identificamos los elementos del DOM
    var themeToggleDarkIcon = document.getElementById('theme-toggle-dark-icon');
    var themeToggleLightIcon = document.getElementById('theme-toggle-light-icon');
    var themeToggleBtn = document.getElementById('theme-toggle');

    // 2. Revisar preferencias al cargar la página
    if (localStorage.getItem('color-theme') === 'dark' || (!('color-theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
        themeToggleLightIcon.classList.remove('hidden');
        document.documentElement.classList.add('dark');
    } else {
        themeToggleDarkIcon.classList.remove('hidden');
        document.documentElement.classList.remove('dark');
    }

    // 3. Lógica al hacer clic en el botón
    themeToggleBtn.addEventListener('click', function() {
        // Intercambiar los iconos visualmente
        themeToggleDarkIcon.classList.toggle('hidden');
        themeToggleLightIcon.classList.toggle('hidden');

        // Alternar la clase 'dark' en el HTML y guardar en LocalStorage
        if (localStorage.getItem('color-theme')) {
            if (localStorage.getItem('color-theme') === 'light') {
                document.documentElement.classList.add('dark');
                localStorage.setItem('color-theme', 'dark');
            } else {
                document.documentElement.classList.remove('dark');
                localStorage.setItem('color-theme', 'light');
            }
        } else {
            if (document.documentElement.classList.contains('dark')) {
                document.documentElement.classList.remove('dark');
                localStorage.setItem('color-theme', 'light');
            } else {
                document.documentElement.classList.add('dark');
                localStorage.setItem('color-theme', 'dark');
            }
        }
    });
</script>
Con estas tres piezas, cualquier clase en tu HTML que lleve el prefijo dark: (por ejemplo, dark:bg-gray-900) se activará mágicamente cada vez que presiones el botón.


### Después del prompt la IA me explicó el funcionamiento de el modo oscuro en la página web.


# 2.- ¿Cuál es la diferencia entre Vite y CDN?

1. CDN (Content Delivery Network)
Una CDN es una red de servidores distribuidos por todo el mundo que aloja archivos de código para que los navegadores los descarguen directamente.

Cuando usas Tailwind vía CDN con <script src="[https://cdn.tailwindcss.com](https://cdn.tailwindcss.com)"></script>, tu página web se conecta a internet y descarga todo el motor de Tailwind directamente en el navegador del usuario cada vez que abre la página.

Ventajas:
Configuración en 1 segundo: Solo copias y pegas un enlace en tu HTML y ya puedes empezar a programar.
Sin instalaciones: No necesitas tener Node.js ni instalar paquetes en tu computadora.

Desventajas:
Rendimiento en producción: Descarga una cantidad masiva de código (incluso las clases CSS que no estás usando), lo que hace la página más pesada y lenta de cargar para el usuario final.
Dependencia de internet: Si no tienes conexión a internet mientras programas, los estilos no cargarán en tu computadora.

2. Vite
Vite es una herramienta de construcción (Build Tool) y un servidor de desarrollo local. No es un servidor de internet, sino un programa que corre en tu computadora mientras desarrollas.
Cuando usas Vite, instalas Tailwind localmente en tu proyecto (usando comandos como npm install). Vite lee tu código, detecta exactamente qué clases de Tailwind utilizaste, y "construye" un archivo CSS minúsculo y optimizado solo con lo que necesitas.

Ventajas:
Extremadamente rápido (HMR): Vite actualiza la pantalla de tu navegador en milisegundos en cuanto guardas un cambio en tu código, sin necesidad de recargar la página completa.
Optimización para producción: Al momento de subir tu página, Vite comprime tus archivos HTML, CSS y JavaScript para que pesen lo mínimo indispensable, haciendo que tu web cargue a la velocidad de la luz.

Desventajas:
Curva de aprendizaje: Requiere instalar Node.js, usar la terminal, y configurar archivos (como vite.config.js y tailwind.config.js).

# Wireframes
Para los wireframes se utilizó la AI integrada de Figma.

# Tailwind
Al trabajar con Tailwind por mi cuenta, entendí realmente la gran ventaja de darle estilo a la página directo en el HTML, sin tener que depender de un archivo CSS aparte. Aunque al principio cuesta un poco aprenderse tantas clases de memoria, me di cuenta de que vale mucho la pena porque evita que los estilos choquen entre sí y desordenen la página. Además, vi lo fácil que es hacer que el diseño se adapte a celulares o pantallas grandes usando solo sus prefijos (como sm: o md:), en lugar de tener que configurar todo eso a mano paso a paso.