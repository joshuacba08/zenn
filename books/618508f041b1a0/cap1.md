---
title: "Introducción al arte generativo con JavaScript
---

En este capítulo tendremos nuestro primer contacto con el arte generativo utilizando JavaScript. Además veremos algunos ejemplos básicos y abordaremos las herramientas necesarias para comenzar a crear nuestras propias obras de arte generativo.

Siéntete libre de experimentar con los ejemplos y modificar el código para entender mejor cómo funciona el arte generativo.

## ¿Qué es el arte generativo?

Antes de empezar, me gustaría dejar en claro qué es y qué no es el arte generativo. La palabra ARTE y la palabra GENERATIVO son dos palabras que pueden tener muchas interpretaciones por sí solas, dependiendo del contexto en el que se usen.

En programación, el término "generativo" se refiere a la capacidad de un sistema para crear contenido de manera autónoma, siguiendo ciertas reglas o algoritmos predefinidos. En el contexto del arte, el arte generativo es una forma de arte que utiliza sistemas autónomos para generar obras de arte. Estos sistemas pueden incluir algoritmos, reglas matemáticas, inteligencia artificial, entre otros.

Me gustaría que observes algunos ejemplos de Arte Generativo en los siguientes enlaces:

- [OpenProcessing](https://openprocessing.org)Plataforma comunitaria donde artistas y devs suben proyectos hechos con **p5.js (Processing en JavaScript)**.Puedes ver el código, modificarlo y remezclarlo.
- [Processing Foundation](https://processing.org)El corazón del movimiento de arte generativo. Recursos, ejemplos y proyectos hechos con **Processing**, pionero en arte computacional.
- [Generative Hut](https://generativehut.com)Comunidad y blog con proyectos de **arte generativo, plotters y algoritmos visuales**.
- [Art Blocks](https://www.artblocks.io)Plataforma de **arte generativo en blockchain**. Catálogo de artistas que usan algoritmos para crear obras únicas.
- [Algorithmic Art Assembly](https://aaassembly.org/)
  Archivo online de charlas y performances sobre **arte generativo, sonido y visuales en vivo**.

![Algunos proyectos de arte generativo](https://res.cloudinary.com/dvgro0geg/image/upload/v1758448491/assets/generative_art/Captura_de_pantalla_septiembre_21_2025_06_54_33_fxiq6d.jpg)

Espero que tu impresión inicial sea de asombro y curiosidad como lo fue para mí cuando descubrí este fascinante mundo del arte generativo. Créeme que en este libro te voy a guiar paso a paso para que puedas crear tus propias obras de arte generativo utilizando JavaScript.

## Herramientas necesarias

Para seguir los ejemplos y crear tus propias obras de arte generativo, necesitarás algunas herramientas básicas:

1. **Editor de código**: Puedes usar cualquier editor de código que prefieras, como Visual Studio Code, Firebase Studio, Cursor, entre otros. También puedes usar editores en línea como StackBlitz o CodeSandbox. En mi caso usaré Visual Studio Code que es el más común y popular entre desarrolladores.
2. **Navegador web**: Un navegador moderno como Google Chrome, Firefox o Edge para ejecutar y visualizar tus proyectos. En mi caso usaré Microsoft Edge por su función de Vista 3D integrada.
3. **Servidor local**: Para ejecutar tus proyectos de manera local, puedes usar extensiones como "Live Server" en Visual Studio Code o herramientas como Node.js con Express. En mi caso usaré la extensión Live Server de Visual Studio Code.

> **Agentes de IA**: La nueva forma de programar incluye asistentes de inteligencia artificial como GitHub Copilot, Claude, Gemini entre otros. Muchos corriendo dentro de un editor de código como el de cursor por ejemplo. Sin embargo, al menos en los primeros capítulos de este libro, te recomiendo deshabilitarlos para que puedas aprender los conceptos básicos y tengas una comprensión sólida de cómo funciona el arte generativo con JavaScript. Luego, incluso si piensas usar un agente de IA, verás que tus prompts serán mucho más efectivos si tienes una buena base de conocimientos.

## Bibliotecas de JavaScript para arte generativo

Para facilitar la creación de arte generativo con JavaScript y no empezar todo desde cero, existen varias bibliotecas que puedes utilizar. Voy a nombrarte los más populares y de los cuales usarémos algunos en este libro:

- **p5.js**: Una biblioteca de JavaScript que hace que la programación creativa sea accesible para artistas, diseñadores y principiantes. Proporciona una forma sencilla de dibujar gráficos, manejar interacciones y trabajar con multimedia. [Sitio oficial](https://p5js.org)
- **Three.js**: Una biblioteca de JavaScript que facilita la creación y visualización de gráficos 3D en el navegador. Es muy potente y ampliamente utilizada para proyectos de arte generativo en 3D. [Sitio oficial](https://threejs.org)
- **D3.js**: Una biblioteca para manipular documentos basados en datos. Es muy útil para crear visualizaciones de datos interactivas y dinámicas. [Sitio oficial](https://d3js.org)
- **Paper.js**: Una biblioteca de gráficos vectoriales que facilita la creación de gráficos y animaciones. [Sitio oficial](http://paperjs.org)
- **Canvas API**: Una API nativa de HTML5 que permite dibujar gráficos y animaciones directamente en un elemento `<canvas>`. No es una biblioteca, pero es fundamental para entender cómo funciona el dibujo en la web. [Documentación MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
- **p5.js WebGL**: Una extensión de p5.js que permite trabajar con gráficos 3D utilizando WebGL. [Documentación oficial](https://p5js.org/reference/#/p5/createCanvas)
- **Tone.js**: Una biblioteca para crear y manipular sonidos en la web, útil para proyectos de arte generativo que incluyen audio. [Sitio oficial](https://tonejs.github.io)
- **Zdog**: Una biblioteca de gráficos 3D en JavaScript que facilita la creación de ilustraciones y animaciones en 3D con un enfoque en la simplicidad y el diseño. [Sitio oficial](https://zzz.dog)

Aunque existen muchas más, estas son algunas de las más populares y ampliamente utilizadas en la comunidad de desarrolladores que aman el arte generativo. A lo largo de este libro, exploraremos algunas de estas bibliotecas y aprenderemos a utilizarlas para crear nuestras propias obras de arte generativo.

## ¿Puedo prescindir de las bibliotecas?

Muchas veces, cuando empezamos a programar, queremos hacerlo todo desde cero para entender mejor cómo funcionan las cosas. Y está perfecto. Sin embargo, en el caso del arte generativo, usar bibliotecas como p5.js o Three.js nos permite enfocarnos más en la creatividad y menos en los detalles técnicos. Estas bibliotecas ya tienen muchas funciones y herramientas integradas que facilitan la creación de gráficos, animaciones e interacciones.

Así que, todo dependerá de tu perfil y tus objetivos. Si quieres reforzar tus conocimientos de JavaScript y entender cómo funcionan las cosas a un nivel más bajo, puedes intentar crear algunos proyectos sin bibliotecas. Pero si tu objetivo principal es crear arte generativo de manera rápida y eficiente, te recomiendo usar estas bibliotecas o incluso crear tus propias funciones reutilizables. Al final del día, lo más importante es que disfrutes el proceso de creación y experimentación con el arte generativo.

## Primer ejemplo con p5.js

Antes que nada quiero que tengas tu primer contacto con la generación de arte con código, y es que una vez que veas el enorme potencial que tiene, no querrás dejar de experimentar.

Te imaginas poder expresar formulas matemáticas, física, geometría y más a través de visualizaciones interactivas y dinámicas? Con p5.js, esto es posible y muy accesible. En nuestro primer ejemplo, vamos a representar la orbita de la luna alrededor de la tierra, y la tierra alrededor del sol. Un sistema simple pero que nos permitirá entender cómo funcionan las órbitas y las relaciones entre los cuerpos celestes.

### Moon path (modelo heliocéntrico simplificado)

Si bien sabemos que las orbitas de los planetas y satélites no son perfectamente circulares, para este ejemplo simplificado, asumiremos que tanto la órbita de la Tierra alrededor del Sol como la órbita de la Luna alrededor de la Tierra son circulares. Esto nos permitirá centrarnos en los conceptos básicos sin complicarnos con las excentricidades orbitales.

![Órbita de la luna alrededor de la tierra y la tierra alrededor del sol](https://res.cloudinary.com/dvgro0geg/image/upload/v1759597049/assets/generative_art/859bc24e-ed65-4a66-9e9a-baec5b8baa96.png)

Para este primer ejemplo, usaremos el editor en línea de p5.js, que puedes encontrar en [editor.p5js.org](https://editor.p5js.org). Aquí tienes el código para dibujar la órbita de la luna alrededor de la tierra y la tierra alrededor del sol:

```javascript
// Cap.1 – Moon Path: trayectoria de la Luna (modelo heliocéntrico simple)
// Visual: trail con degradado sobre fondo oscuro, Tierra y Luna animadas.

const CFG = {
  earthRadiusOrb: 280, // radio de la órbita de la Tierra (px)
  moonRadiusOrb: 90, // radio de la órbita de la Luna alrededor de la Tierra (px)
  earthPeriod: 365.0, // periodo Tierra (unidades de tiempo)
  moonPeriod: 27.32, // periodo Luna (unidades de tiempo)
  speed: 0.8, // velocidad de simulación (frames/unidad)
  trailMax: 3200, // cantidad máxima de puntos en el trazo
};

let t = 0; // tiempo simulado
let trail = []; // cola con posiciones de la Luna
let fontReady = false;

function setup() {
  createCanvas(1000, 1000);
  pixelDensity(2);
  colorMode(HSL, 360, 100, 100, 1);
  strokeCap(ROUND);
}

function draw() {
  background(220, 10, 8); // negro suave

  translate(width / 2, height / 2);

  // Sol (disco tenue + glow)
  noStroke();
  for (let r = 160; r >= 0; r -= 8) {
    const a = map(r, 0, 160, 0.8, 0.0);
    fill(45, 95, 60, a * 0.12);
    circle(0, 0, r * 2);
  }

  // Posiciones (modelo circular básico)
  const thetaE = TWO_PI * (t / CFG.earthPeriod);
  const earth = createVector(
    CFG.earthRadiusOrb * cos(thetaE),
    CFG.earthRadiusOrb * sin(thetaE)
  );

  const thetaM = TWO_PI * (t / CFG.moonPeriod);
  const moon = p5.Vector.add(
    earth,
    createVector(
      CFG.moonRadiusOrb * cos(thetaM),
      CFG.moonRadiusOrb * sin(thetaM)
    )
  );

  // Actualizar trail
  trail.push(moon.copy());
  if (trail.length > CFG.trailMax) trail.shift();

  // Dibujar trail con degradado SCREEN
  blendMode(SCREEN);
  noFill();
  const w0 = 2.0;
  for (let i = 1; i < trail.length; i++) {
    const p0 = trail[i - 1];
    const p1 = trail[i];
    const k = i / (trail.length - 1); // 0..1
    const col = lerpColor(color(165, 70, 65, 0.2), color(25, 75, 70, 0.8), k);
    stroke(col);
    strokeWeight(w0);
    line(p0.x, p0.y, p1.x, p1.y);
  }
  blendMode(BLEND);

  // Tierra (esfera con aro)
  push();
  translate(earth.x, earth.y);
  drawPlanet(24, color(205, 60, 55), color(205, 60, 25), 0.35);
  pop();

  // Luna
  push();
  translate(moon.x, moon.y);
  drawPlanet(10, color(0, 0, 90), color(0, 0, 65), 0.25);
  pop();

  // Avanzar tiempo
  t += CFG.speed;

  // Etiquetas
  resetMatrix();
  fill(0, 0, 100, 0.8);
  noStroke();
  rect(16, height - 36, 320, 24, 6);
  fill(220, 10, 8);
  textSize(12);
  textAlign(LEFT, CENTER);
  text(
    "Moon Path (heliocéntrico) · arrastrá para pausar/continuar",
    24,
    height - 24
  );
}

// Planeta con ligero brillo y aro
function drawPlanet(r, fillColor, rimColor, rimAlpha) {
  noStroke();
  fill(fillColor);
  circle(0, 0, r * 2);

  // aro brillante
  stroke(rimColor);
  strokeWeight(3);
  stroke(hue(rimColor), saturation(rimColor), lightness(rimColor), rimAlpha);
  noFill();
  ellipse(0, 0, r * 2.7, r * 0.9);

  // highlight
  noStroke();
  fill(0, 0, 100, 0.25);
  ellipse(-r * 0.4, -r * 0.3, r * 1.2, r * 0.8);
}

// Click/tap para pausar/continuar
function mousePressed() {
  if (isLooping()) noLoop();
  else loop();
}
```

Puedes copiar y pegar este código en el editor de p5.js y hacer clic en el botón de reproducción para ver la simulación en acción. La Tierra orbita alrededor del Sol, y la Luna orbita alrededor de la Tierra, dejando un rastro que muestra su trayectoria.

Si arrastras con el mouse o tocas la pantalla, puedes pausar y reanudar la animación. Experimenta con el código, cambia los parámetros y observa cómo afectan la simulación. ¡Diviértete explorando el arte generativo con JavaScript!

## Conceptos clave

Mientras empezamos a introducirnos en el arte generativo con JavaScript, es importante entender algunos conceptos clave que nos ayudarán a entender e identificar patrones en el código y en la lógica detrás de nuestras creaciones. Aquí hay algunos conceptos que veremos a lo largo del libro:

### 1. Semilla (seed)

Una semilla es un valor inicial que se utiliza para generar números aleatorios de manera reproducible, es decir, es el valor que controla la aleatoriedad. En el arte generativo, las semillas permiten crear variaciones de una obra manteniendo ciertos elementos constantes. Cambiar la semilla puede dar lugar a resultados completamente diferentes.

#### Laboratorio: Tus primeras variaciones

Empieza a probar cambiando algunos valores del código del ejemplo de arriba:

```javascript
moonPeriod: 27.32, // periodo Luna (unidades de tiempo)
moonDistance: 384400, // distancia Tierra-Luna (en km)
```

Verás que al cambiar estos valores, la órbita de la Luna y su velocidad cambian, creando diferentes patrones y trayectorias. Pues bién, esto claramente es un ejemplo de cómo una semilla (en este caso los valores de periodo y distancia) puede influir en el resultado final de una obra generativa.

## ¿Cómo aprender a programar en la era moderna?

Bien, ya hemos visto un primer ejemplo de arte generativo con JavaScript utilizando p5.js. A medida que avancemos en este libro, exploraremos más ejemplos y técnicas para crear obras de arte generativo cada vez más complejas e interesantes, pero antes de continuar, quiero compartir contigo algunas reflexiones sobre el camino del principiante moderno en plena era de librerías, frameworks y agentes de IA que nos asisten en la programación.

Soy consciente de que la manera en la que aprendí a programar hace unos años es muy diferente a la forma en la que los nuevos desarrolladores lo hacen hoy en día. Lo veo mucho durante mis clases y talleres. Y no es ni mejor ni peor, simplemente es diferente. Hace 5 años, mis alumnos tenían problemas y desafíos en su aprendizaje, las cuales eran diferentes a las que yo tuve pero que sin embargo pudieron superar. Lo cierto es que hoy en día, mis nuevos alumnos a pesas de contar con más recursos y herramientas, también enfrentan sus propios desafíos.

¿A qué quiero llegar con esto? A que no importa la época en la que aprendas a programar, siempre habrá desafíos y obstáculos que superar. Y eso está bien. Lo importante es tener la actitud correcta y estar dispuesto a aprender y adaptarse. Así que al igual que hice con mis alumnos de hace 5 años, quiero compartir contigo algunos consejos y reflexiones que te ayudarán en tu camino como principiante moderno en el mundo de la programación y el arte generativo.

1. **Aprende los fundamentos**: Aunque hoy en día hay muchas herramientas y librerías que facilitan la programación, es fundamental entender los conceptos básicos. Esto te permitirá resolver problemas de manera más efectiva y adaptar las herramientas a tus necesidades.

2. **Experimenta y juega**: No tengas miedo de experimentar con el código. La programación es un proceso creativo, y a menudo las mejores ideas surgen de la exploración y el juego. Prueba cosas nuevas, rompe el código y aprende de los errores.

3. **Busca inspiración**: El arte generativo es un campo en constante evolución. Busca inspiración en el trabajo de otros artistas y programadores. Estudia sus técnicas y trata de entender cómo lograron ciertos efectos.

4. **Colabora y comparte**: La comunidad de programación es muy activa y solidaria. No dudes en colaborar con otros, compartir tus proyectos y pedir ayuda cuando la necesites. Aprender de los demás es una de las mejores maneras de crecer como programador.

5. **Mantente actualizado**: La tecnología avanza rápidamente, y es importante mantenerse al día con las últimas tendencias y herramientas. Sigue aprendiendo y explorando nuevas tecnologías que puedan enriquecer tu práctica artística.

Me encantaría que tomes estos consejos y reflexiones como una guía para tu propio camino no solo en el mundo del arte generativo, sino en cualquier área de la programación que decidas explorar. Recuerda que el aprendizaje es un viaje continuo, y cada paso que das te acerca más a tus objetivos. **No te abstraigas de los desafíos, abrázalos y aprende de ellos.**

## Resumen del capítulo

En este capítulo, hemos introducido el concepto de arte generativo y las herramientas necesarias para comenzar a crear nuestras propias obras utilizando JavaScript. Hemos explorado algunas de las bibliotecas más populares para el arte generativo y hemos visto un primer ejemplo práctico utilizando p5.js para simular la órbita de la Luna alrededor de la Tierra y la Tierra alrededor del Sol.

Además, hemos reflexionado sobre el camino del principiante moderno en la programación, destacando la importancia de aprender los fundamentos, experimentar, buscar inspiración, colaborar y mantenerse actualizado.

Espero haberte motivado para continuar adentrándote en el contenido de este libro y descubrir todo lo que puedes lograr con el arte generativo y JavaScript. Vamos a seguir explorando más ejemplos y técnicas en los próximos capítulos. ¡Nos vemos allí!
