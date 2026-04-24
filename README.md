# 🧠 Brain Games
### Una colección de mini-juegos de lógica y matemáticas para la línea de comandos

---

## 📖 Sobre el Proyecto

**Brain Games** es una aplicación CLI interactiva que desafía al usuario con una serie de puzzles matemáticos en la terminal. El jugador debe responder correctamente **3 rondas consecutivas** para ganar cada juego.

El proyecto nació como ejercicio fundamental de programación: aprender a **estructurar una aplicación modular desde cero**, separando la lógica de juego de la capa de interacción con el usuario. Cada mini-juego es un módulo independiente que se conecta a un archivo central (src/index.js), demostrando principios de diseño limpio y separación de responsabilidades.

---

## 🛠️ Tecnologías Utilizadas

![JavaScript](https://img.shields.io/badge/JavaScript-ES2020-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-CLI-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![ESLint](https://img.shields.io/badge/ESLint-Airbnb-4B32C3?style=for-the-badge&logo=eslint&logoColor=white)

| Herramienta | Uso |
|---|---|
| `Node.js` (ESModules) | Runtime y sistema de módulos `import/export` |
| `readline-sync` | Captura de input del usuario de forma síncrona en CLI |
| `ESLint` + Airbnb config | Calidad y consistencia del código |

---

## 🎮 Características Principales

- **5 juegos independientes**, cada uno con su propio ejecutable CLI:
  - `brain-even` — ¿Es el número par o impar?
  - `brain-calc` — Calcula el resultado de una operación aritmética (`+`, `-`, `*`)
  - `brain-gcd` — Encuentra el Máximo Común Divisor de dos números
  - `brain-progression` — Adivina el número faltante en una progresión aritmética
  - `brain-prime` — ¿Es el número primo?
- **Archivo de juego centralizado** (`src/index.js`) que gestiona el flujo de 3 rondas para todos los juegos
- **Saludo personalizado** al inicio de cada sesión con el nombre del jugador
- **Feedback inmediato**: el juego muestra la respuesta correcta si el usuario falla
- **Arquitectura modular**: cada juego exporta únicamente su lógica (`gameLogic`) y su `description`, sin acoplamiento

---

## ⚙️ Instalación y Configuración

### Pre-requisitos

- `Node.js` v16 o superior
- `npm` v8 o superior

### Pasos

```bash
# 1. Clona el repositorio
git clone https://github.com/Porico94//Proyecto-Juegos-Mentales

# 2. Entra al directorio
cd brain-games

# 3. Instala las dependencias
npm install

# 4. Vincula los ejecutables de forma global (opcional)
npm link
```

### Ejecutar los juegos

```bash
# Juego de paridad
brain-even

# Calculadora mental
brain-calc

# Máximo Común Divisor
brain-gcd

# Progresión aritmética
brain-progression

# Número primo
brain-prime
```

### Ejemplo de sesión

```
¡Bienvenidos a Brain Games!
Cuál es tu nombre: Juan
¡Hola, Juan!
¿Cuál es el resultado de la expresión?
Pregunta: 34 * 12
Tu respuesta: 408
¡Correcto!
Pregunta: 7 + 19
Tu respuesta: 26
¡Correcto!
Pregunta: 45 - 8
Tu respuesta: 37
¡Correcto!
¡Felicidades, Juan!
```

---

## 💡 Aprendizajes

> ### 🏆 El reto técnico: diseñar un archivo central reutilizable para múltiples juegos

El desafío central de este proyecto no fue implementar los juegos en sí, sino **evitar la duplicación de código** entre los 5 mini-juegos. La primera aproximación ingenua era escribir el loop de 3 rondas, el saludo y el manejo de respuestas en cada archivo `bin/` por separado.

La solución fue extraer todo ese flujo a la función `runGame` en `src/index.js`, que acepta dos parámetros: `gameLogic` (una función que genera pregunta y respuesta correcta) y `gameDescription` (el texto de instrucciones). Cada juego simplemente implementa ese **contrato** y delega el control al archivo central:

```javascript
// src/index.js — El archivo central
const runGame = (gameLogic, gameDescription) => {
  // ...saludo, loop de 3 rondas, feedback... todo aquí
  for (let i = 0; i < maxRounds; i += 1) {
    const { question, correctAnswer } = gameLogic(); // ← contrato
    // ...
  }
};

// bin/brain-prime.js — El juego solo aporta su lógica
import { isPrime, description } from '../src/games/isPrime.js';
import runGame from '../src/index.js';
runGame(isPrime, description); // ← 3 líneas y listo
```

Esto me enseñó el principio de **separación de responsabilidades (SoC)** de forma muy concreta: la lógica matemática de cada juego no debe saber nada sobre cómo se le presenta al usuario. Un concepto que aplico directamente hoy en mis proyectos React al separar la lógica de negocio de los componentes de presentación.

---

## 📂 Estructura del Proyecto

```
brain-games/
├── bin/                      # Ejecutables CLI (entry points)
│   ├── brain-calc.js
│   ├── brain-even.js
│   ├── brain-gcd.js
│   ├── brain-prime.js
│   └── brain-progression.js
├── src/
│   ├── games/                # Lógica de cada juego (módulos independientes)
│   │   ├── arithmeticProgress.js
│   │   ├── calculator.js
│   │   ├── isPrime.js
│   │   ├── mcd.js
│   │   └── parityCheck.js
│   ├── cli.js                # Módulo de saludo/bienvenida
│   └── index.js              # Engine central del juego
├── .eslintrc.yml
└── package.json
```

---

## 👤 Autor

**Pool Rimari** — Desarrollador Full-stack JavaScript

[![GitHub](https://img.shields.io/badge/GitHub-Porico94-181717?style=flat&logo=github)](https://github.com/Porico94)
