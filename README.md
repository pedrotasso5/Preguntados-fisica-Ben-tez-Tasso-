# Preguntados-fisica-Bentez-Tasso
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Preguntados Marino: MRU</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      background: linear-gradient(135deg, #a0e7e5, #b4f8c8);
      margin: 0; padding: 0;
      color: #003f5c;
    }
    .container {
      max-width: 700px;
      margin: 2rem auto;
      background: rgba(255, 255, 255, 0.95);
      padding: 2rem;
      border-radius: 15px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
      text-align: center;
    }
    h1 {
      color: #008891;
      font-size: 2.2rem;
      margin-bottom: 1rem;
    }
    .question {
      font-size: 1.3rem;
      margin: 1.5rem 0;
    }
    .btn {
      margin: 0.5rem 1rem;
      padding: 0.8rem 1.8rem;
      font-size: 1rem;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: transform 0.15s;
    }
    .btn:hover {
      transform: scale(1.1);
    }
    .btn-true {
      background-color: #00c9a7;
      color: white;
    }
    .btn-false {
      background-color: #f45b69;
      color: white;
    }
    .score {
      margin-top: 1.5rem;
      font-size: 1.2rem;
    }
    .final {
      margin-top: 1.5rem;
      font-size: 1.4rem;
      font-weight: bold;
      color: #145374;
    }
    .ocean-icons {
      margin-top: 2rem;
      font-size: 2.2rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>⚓ Preguntados Marino: MRU 🔱</h1>
    <div class="question" id="question">Cargando pregunta...</div>
    <button class="btn btn-true" onclick="answer(true)">✅ Verdadero</button>
    <button class="btn btn-false" onclick="answer(false)">❌ Falso</button>
    <div class="score" id="score">Puntaje: 0</div>
    <div class="final" id="final"></div>
    <div class="ocean-icons">⚓🐟🐚🧜‍♂️🔱🐬🌊</div>
  </div>
  <script>
    const questions = [
      { text: "En MRU, la velocidad es constante.", correct: true },
      { text: "MRU significa Movimiento Rápido Uniforme.", correct: false },
      // ... (incluí las 50 preguntas dentro del array en este formato)
    ];
    let current = 0, score = 0;
    function loadQuestion() {
      if (current < questions.length) {
        document.getElementById('question').innerText = questions[current].text;
      } else {
        document.getElementById('question').style.display = 'none';
        document.querySelector('.btn-true').style.display = 'none';
        document.querySelector('.btn-false').style.display = 'none';
        document.getElementById('final').innerText = `🐬 ¡Juego terminado! Puntaje final: ${score} / ${questions.length}`;
      }
    }
    function answer(userAnswer) {
      if (questions[current].correct === userAnswer) score++;
      current++;
      document.getElementById('score').innerText = `Puntaje: ${score}`;
      loadQuestion();
    }
    loadQuestion();
  </script>
</body>
</html>
