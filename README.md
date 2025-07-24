# Preguntados-fisica-Bentez-Tasso
<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Preguntados Marino: MRU</title>
  <style>
    body {
      background: linear-gradient(to bottom, #a8e0ff, #70cad1);
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 20px;
      color: #00334e;
    }
    .container {
      background: white;
      border-radius: 20px;
      padding: 30px;
      max-width: 600px;
      margin: auto;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
    }
    h1 {
      color: #0077b6;
    }
    button {
      font-size: 18px;
      margin: 10px;
      padding: 10px 20px;
      border-radius: 10px;
      border: none;
      cursor: pointer;
      transition: 0.3s;
    }
    .true-btn {
      background-color: #38b000;
      color: white;
    }
    .false-btn {
      background-color: #d90429;
      color: white;
    }
    .true-btn:hover, .false-btn:hover {
      opacity: 0.8;
    }
    .marine-icons {
      font-size: 24px;
    }
    #feedback {
      margin-top: 20px;
      font-weight: bold;
      color: #005f73;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1 class="marine-icons">⚓ Preguntados Marino: MRU 🐠</h1>
    <p id="question">Cargando pregunta...</p>
    <button class="true-btn" onclick="checkAnswer(true)">✔️ Verdadero</button>
    <button class="false-btn" onclick="checkAnswer(false)">❌ Falso</button>
    <p>Puntaje: <span id="score">0</span></p>
    <p id="feedback"></p>
  </div>  <script>
    const questions = [
      { q: "En MRU, la velocidad es constante.", a: true, e: "Correcto. En MRU, la velocidad no cambia con el tiempo." },
      { q: "En MRU, hay aceleración.", a: false, e: "Incorrecto. En MRU la aceleración es cero." },
      { q: "La fórmula del MRU es d = v * t.", a: true, e: "Correcto. Esta fórmula se usa para calcular la distancia." },
      { q: "En MRU, la velocidad cambia con el tiempo.", a: false, e: "Incorrecto. La velocidad en MRU es constante." },
      { q: "En MRU, la trayectoria es recta.", a: true, e: "Correcto. El movimiento es rectilíneo, por definición." },
      { q: "Si la velocidad es negativa, el objeto se detiene.", a: false, e: "Falso. Solo indica que el movimiento es en sentido contrario." },
      { q: "El tiempo influye en la distancia en MRU.", a: true, e: "Sí. A mayor tiempo, mayor distancia recorrida si la velocidad es constante." },
      { q: "En MRU, el objeto está en reposo.", a: false, e: "Falso. Está en movimiento constante, no quieto." },
      { q: "La distancia y el desplazamiento siempre son iguales en MRU.", a: false, e: "No siempre. Solo si no hay cambio de dirección." },
      { q: "MRU significa Movimiento Relativamente Uniforme.", a: false, e: "Falso. Significa Movimiento Rectilíneo Uniforme." },
      { q: "El MRU tiene aceleración distinta de cero.", a: false, e: "Incorrecto. En MRU la aceleración es cero." },
      { q: "Un auto que se mueve a 60 km/h por 2 horas recorre 120 km.", a: true, e: "Correcto. v × t = 60 × 2 = 120 km." },
      { q: "La distancia recorrida depende solo de la velocidad.", a: false, e: "Falso. Depende de la velocidad y el tiempo." },
      { q: "La aceleración es necesaria para que haya MRU.", a: false, e: "Falso. La aceleración debe ser cero." },
      { q: "La gráfica de velocidad vs tiempo en MRU es una recta horizontal.", a: true, e: "Correcto. La velocidad no cambia." },
      { q: "El área bajo la curva de velocidad vs tiempo representa la distancia.", a: true, e: "Correcto. En MRU, área = d." },
      { q: "La aceleración en MRU es constante y distinta de cero.", a: false, e: "Incorrecto. Es constante pero es cero." },
      { q: "Una bicicleta que mantiene su velocidad está en MRU.", a: true, e: "Correcto. Mantener velocidad = MRU." },
      { q: "En MRU, la rapidez cambia constantemente.", a: false, e: "Falso. La rapidez es constante." },
      { q: "El MRU es un tipo de movimiento uniforme.", a: true, e: "Correcto. Es el movimiento más básico uniforme." },
      { q: "Si t = 0, la distancia también es cero en MRU.", a: true, e: "Correcto. d = v × 0 = 0." },
      { q: "Si v = 0, el objeto está en MRU.", a: false, e: "Falso. Si v = 0, está en reposo absoluto." },
      { q: "La unidad de velocidad en el SI es m/s.", a: true, e: "Correcto. El Sistema Internacional usa m/s." },
      { q: "En MRU, la dirección del movimiento cambia.", a: false, e: "Falso. La dirección es constante." },
      { q: "La pendiente en una gráfica de posición vs tiempo es la velocidad.", a: true, e: "Correcto. Pendiente = velocidad en MRU." },
      { q: "El MRU no existe en la vida real.", a: false, e: "Falso. Hay muchos ejemplos aproximados, como trenes o cintas transportadoras." },
      { q: "La velocidad puede medirse con un velocímetro.", a: true, e: "Correcto. Es el instrumento para ello." },
      { q: "La distancia en MRU se mide en newtons.", a: false, e: "Incorrecto. Se mide en metros." },
      { q: "Un móvil con velocidad constante no cambia su posición.", a: false, e: "Falso. Cambia su posición uniformemente." },
      { q: "Para calcular tiempo en MRU usamos t = d/v.", a: true, e: "Correcto. Es la fórmula derivada de d = v × t." },
      { q: "MRU y MRUV son lo mismo.", a: false, e: "Falso. MRU no tiene aceleración, MRUV sí." },
      { q: "El tiempo siempre va hacia adelante en MRU.", a: true, e: "Correcto. No retrocede en física clásica." },
      { q: "La velocidad puede ser positiva o negativa.", a: true, e: "Correcto. Depende del sentido del movimiento." },
      { q: "Un objeto que retrocede a velocidad constante está en MRU.", a: true, e: "Sí. MRU permite velocidades negativas." },
      { q: "Un objeto con trayectoria circular está en MRU.", a: false, e: "Falso. La trayectoria debe ser recta." },
      { q: "Se puede tener MRU en el espacio.", a: true, e: "Correcto. Si no hay fuerzas, se conserva el MRU." },
      { q: "Un avión con velocidad constante realiza MRU.", a: true, e: "Correcto. Si no cambia ni dirección ni velocidad." },
      { q: "La velocidad escalar y vectorial son lo mismo.", a: false, e: "Falso. La escalar no tiene dirección." },
      { q: "La fórmula d = v × t solo sirve en MRUV.", a: false, e: "Falso. Es válida en MRU." },
      { q: "Una velocidad negativa significa que el objeto se detuvo.", a: false, e: "Incorrecto. Indica que va en sentido opuesto." },
      { q: "MRU es más simple que el MRUV.", a: true, e: "Correcto. Tiene menos variables (sin aceleración)." },
      { q: "Un robot que avanza 1 metro por segundo está en MRU.", a: true, e: "Correcto. Velocidad constante." },
      { q: "Un movimiento con aceleración creciente es MRU.", a: false, e: "Falso. Eso es MRUV." },
      { q: "Si la velocidad aumenta, no es MRU.", a: true, e: "Correcto. En MRU no cambia la velocidad." },
      { q: "La unidad de tiempo en MRU puede ser horas o segundos.", a: true, e: "Correcto. Lo importante es mantener coherencia." },
      { q: "La rapidez se mide en metros por segundo.", a: true, e: "Correcto. Es una magnitud escalar." },
      { q: "En MRU no se necesita energía.", a: false, e: "Falso. Todo movimiento requiere energía inicial." },
      { q: "La posición siempre aumenta en MRU.", a: false, e: "Falso. Puede disminuir si la velocidad es negativa." },
      { q: "La aceleración puede cambiar en MRU.", a: false, e: "Falso. La aceleración es nula y constante." },
      { q: "MRU es útil para predecir posiciones futuras.", a: true, e: "Correcto. Se puede calcular d = v × t fácilmente." }
    ];

    let current = 0;
    let score = 0;

    function loadQuestion() {
      document.getElementById("question").innerText = questions[current].q;
      document.getElementById("feedback").innerText = "";
    }

    function checkAnswer(userAnswer) {
      const correct = questions[current].a;
      if (userAnswer === correct) {
        score++;
      }
      document.getElementById("score").innerText = score;
      document.getElementById("feedback").innerText = questions[current].e;
      current++;
      if (current < questions.length) {
        setTimeout(loadQuestion, 1500);
      } else {
        setTimeout(() => {
          document.getElementById("question").innerText = "¡Juego terminado!";
          document.getElementById("feedback").innerText = "Puntaje final: " + score + "/" + questions.length;
        }, 1500);
      }
    }

    loadQuestion();
  </script></body>
</html>
