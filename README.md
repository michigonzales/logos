<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Círculo Interactivo</title>

  <style>
    /* Estilos generales del cuerpo */
    body {
      margin: 0; /* Quita el margen por defecto del body */
      background-color: #2c3e50; /* Color de fondo oscuro */
      cursor: none; /* Oculta el cursor para mejorar el efecto del seguidor */
      overflow: hidden; /* Oculta las barras de desplazamiento */
    }

    /* Estilos del círculo que sigue al mouse */
    #circle {
      position: fixed; /* Posición fija para que se mueva con el viewport */
      width: 40px; /* Ancho inicial del círculo */
      height: 40px; /* Alto inicial del círculo */
      background-color: #3498db; /* Color azul inicial */
      border-radius: 50%; /* Hace que el div sea un círculo */
      transform: translate(-50%, -50%); /* Centra el círculo en su punto (no desde la esquina) */
      transition: transform 0.1s ease, background-color 0.3s ease; /* Transiciones suaves para tamaño y color */
      pointer-events: none; /* Hace que el círculo no bloquee clics o eventos del mouse */
      z-index: 9999; /* Asegura que el círculo esté por encima de todos los elementos */
    }
  </style>
</head>
<body>

  <!-- Elemento que actuará como el círculo interactivo -->
  <div id="circle"></div>

  <script>
    // Obtiene el elemento del DOM con id "circle"
    const circle = document.getElementById('circle');

    // Array de colores que usaremos para cambiar al hacer clic
    const colors = ['#e74c3c', '#2ecc71', '#f1c40f', '#9b59b6', '#1abc9c', '#e67e22'];

    // Índice actual del color seleccionado en el array
    let currentColorIndex = 0;

    // Estado de tamaño del círculo: false = pequeño, true = grande
    let isLarge = false;

    // Evento que se ejecuta cada vez que el mouse se mueve
    document.addEventListener('mousemove', (event) => {
      // Mueve el círculo a la posición actual del cursor
      circle.style.left = ${event.clientX}px;  // clientX = posición horizontal del mouse
      circle.style.top = ${event.clientY}px;   // clientY = posición vertical del mouse
    });

    // Evento que se ejecuta al hacer clic en cualquier parte de la pantalla
    document.addEventListener('click', () => {
      // Cambia al siguiente color en el array, ciclando si llega al final
      currentColorIndex = (currentColorIndex + 1) % colors.length;
      circle.style.backgroundColor = colors[currentColorIndex]; // Aplica el nuevo color al círculo

      // Cambia el tamaño del círculo: si es grande, lo hace pequeño; si es pequeño, lo agranda
      isLarge = !isLarge; // Invierte el estado

      if (isLarge) {
        // Aumenta el tamaño al doble con transform scale(2)
        circle.style.transform = 'translate(-50%, -50%) scale(2)';
      } else {
        // Restaura el tamaño original con scale(1)
        circle.style.transform = 'translate(-50%, -50%) scale(1)';
      }
    });
  </script>
</body>
</html>
