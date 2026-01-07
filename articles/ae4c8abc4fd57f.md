---
title: "Qué es el principio de incertidumbre de un estado en React"
emoji: "🤔"
type: "tech, idea"
topics: ["react", "javascript", "frontend"]
description: "Cuando un componente React se comporta de manera aleatoria ante cambios de estado, estamos frente a un estado en incertidumbre."
published: true
---

## Principio de incertidumbre de un estado en React

Si has trabajado con React, es probable que hayas tenido problemas con los estados de tus componentes. En este artículo veremos como enfrentar este problema y las distinas formas de solucionarlo.

Hace poco estuve ayudando a un colega con un problema en su aplicación de React. Estaba trabajando con un componente que debía reproducir un video y pausar la reproducción en un segundo determinado. Al principio uno puede pensar que es un problema sencillo, es decir, tienes un simple estado booleano que indica si el video está en reproducción o no. Sin embargo, luego de probar el la aplicación, se dió cuenta que en ocasiones el video no volvía a reproducirse por más lógica que le añadiera, incluso GPT le decía que estaba bien, o añadía más lógica y el problema persistía. Entonces, ¿qué estaba pasando? ¿Por qué no podía hacer que su video se reprodujera nuevamente?

En ese momento dijo una frase que me hizo pensar:

> "Lo ideal sería que mi componente funcione o no funcione, pero... ¡funciona a veces y a veces no!

Esto me hizo reflexionar, ya que es verdad, cuando desarrollamos componentes que responden a un estado para definir su comportamiento, pero estos terminan teniendo un comportamiento errático, tendemos a pensar que se trata de un bug pero no diagnosticamos el problema correctamente.

Si tu código funciona unas veces y otras no, y esto depende de un estado, entonces podemos decir que el estado se encuentra en un (valga a redundancia) estado de incertidumbre. Esto es lo que yo llamo el **principio de incertidumbre de un estado en React**.

Ok, quiza esto suene un poco raro, o tan solo pienses que se trata de un bug y ya. Pero ser concientes de que el problema tiene que ver con que el estado se encuentra en un estado de incertidumbre, nos puede ayudar a encontrar la solución.

## Principio de incertidumbre de un estado en React

> Cuando un componente React se comporta de manera aleatoria ante cambios de estado —funciona a veces y a veces no— estamos frente a un estado en incertidumbre.

Este principio no habla de física cuántica ni del funcionamiento interno de React, sino del momento exacto en que un desarrollador siente que todo está bien en su código, pero el comportamiento no es consistente.

No hay errores visibles, no hay excepciones, y hasta la lógica parece sólida. Pero sin embargo… el componente falla, y lo hace de forma errática. Reproduce un video unas veces sí y otras no. Cambia una clase CSS a veces sí, otras no. La actualización de un booleano simplemente no sucede o si sucede, no se refleja en la UI.

## ¿Por qué sucede esto?

Ahora que hemos diagnosticado que el problema tiene que ver con un estado en incertidumbre, es hora de ver por qué sucede esto.

### 1. El estado no se actualiza

El primer problema que puede suceder es que el estado no se actualiza. Esto puede suceder por varias razones, pero la más común es que el estado no se actualiza de forma síncrona. Esto significa que cuando llamas a `setState`, el nuevo valor del estado no está disponible inmediatamente. En su lugar, React programa una actualización del estado y lo actualiza en un momento posterior. Este es un error muy común sobre todo en principiantes, ya que piensan que el estado se actualiza inmediatamente y no es así.

#### Ejemplo

```typescript
const [isPlaying, setIsPlaying] = useState(false);

const handlePlay = () => {
  setIsPlaying(true);
  console.log("¿Está reproduciendo?", isPlaying); // ❌ Siempre muestra: false
};
const handlePause = () => {
  setIsPlaying(false);
  console.log("¿Está reproduciendo?", isPlaying); // ❌ Siempre muestra: true
};
```

En este ejemplo, el estado `isPlaying` no se actualiza inmediatamente después de llamar a `setIsPlaying`. Por lo tanto, cuando intentamos acceder al valor del estado inmediatamente después de actualizarlo, siempre obtendremos el valor anterior.

#### Solución recomendada

La forma correcta de trabajar con el nuevo valor del estado es esperar a que React haga el render y reaccionar a los cambios con un useEffect:

```typescript
useEffect(() => {
  if (isPlaying) {
    console.log("El video está en reproducción");
    // reproducirVideo(); ← tu lógica aquí
  }
}, [isPlaying]);

const handlePlay = () => {
  setIsPlaying(true);
};
```

> **Nota:** Si necesitás hacer algo en el momento justo en que el estado cambia, no lo hagas inmediatamente después de setState. Usá useEffect para esperar a que el nuevo valor esté disponible tras el render.

### 2. Funciones externas que afectan al estado sin que te des cuenta

A veces no es el setState el que falla, sino una función externa que modifica el valor o el contexto del estado desde afuera, causando que el comportamiento se vuelva errático.

Esto puede pasar cuando:
• Tienes lógica compartida en servicios, utilidades o archivos separados.
• Usas referencias (ref) para acceder al DOM o a valores mutables.
• Tenés callbacks que se ejecutan desde fuera del flujo React (como eventos de terceros o listeners manuales).

#### Ejemplo

```typescript
const [isVisible, setIsVisible] = useState(true);

externalController.onToggle(() => {
  setIsVisible(false); // ❗ Pero no sabés que esto se está llamando en otro archivo
});
```

El estado isVisible cambia “mágicamente”, y tu ni siquiera lo ves en tu componente.

> **Nota:** Este es un error común en aplicaciones grandes, donde el estado se comparte entre varios componentes o servicios. Es importante tener cuidado al modificar el estado desde fuera del flujo de React. (Por cierto, este era el problema de mi colega, el video no se reproducía porque había un listener que lo pausaba desde otro archivo y no se daba cuenta).

#### Solución recomendada: Encapsular la lógica que modifica el estado

Si una función externa necesita modificar el estado, protegé el acceso con una función explícita desde el componente, así controlás cuándo y cómo se cambia:

```typescript
useEffect(() => {
  const handleToggle = () => {
    console.log("Ocultando componente desde controlador externo");
    setIsVisible(false);
  };

  externalController.onToggle(handleToggle);

  return () => {
    externalController.offToggle(handleToggle);
  };
}, []);
```

> **Nota:** En este caso, el efecto se encarga de limpiar el listener cuando el componente se desmonta, evitando que el estado quede en un estado de incertidumbre.

#### Consejo práctico

Si sientes que “el estado cambia solo”, probablemente alguien lo está tocando desde afuera. Audita el código en busca de listeners, servicios o refs que puedan modificarlo por fuera del ciclo de React.

### 3. Estado sincronizado con props que nunca se actualiza

A veces inicializamos un estado en base a una prop, pero esperamos que ese estado se actualice automáticamente cuando la prop cambie… y no lo hace.

Esto pasa mucho cuando el desarrollador copia una prop en un useState y asume que estarán sincronizados para siempre. Spoiler: no lo estarán.

#### Ejemplo

```typescript
const MyComponent = ({ initialValue }) => {
  const [value, setValue] = useState(initialValue);

  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
};
```

Si initialValue cambia desde el componente padre, value no cambia, porque useState solo toma la prop una vez al inicio. Esto puede generar inconsistencias difíciles de detectar, especialmente cuando usás formularios, modales, o entradas controladas.

#### Solución recomendada: Sincronizar el estado con useEffect

```typescript
const MyComponent = ({ initialValue }) => {
  const [value, setValue] = useState(initialValue);

  useEffect(() => {
    setValue(initialValue);
  }, [initialValue]);

  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
};
```

> **Nota:** En este caso, el efecto se encarga de sincronizar el estado con la prop inicial, asegurando que siempre tenga el valor correcto.

> **💡 Consejo práctico**
> Si estás copiando una prop en un state, preguntate:
> “¿Esto debería seguir sincronizado o solo es un valor inicial?”
> Si querés que se mantengan sincronizados, necesitás controlarlo manualmente con useEffect.

Este tipo de errores se manifiestan como: **“mi input no cambia aunque la prop cambió”**, o “el modal no se actualiza cuando cambio los datos”, y pueden ser muy difíciles de diagnosticar si no conocés este patrón.

## Conclusiones

Si has llegado hasta acá, antes que nada quiero agradecerte por dedicarme tu tiempo. Espero que este artículo te esté resultando útil.

- El principio de incertidumbre de un estado en React no es solo una metáfora divertida —es una herramienta mental útil para diagnosticar esos casos donde “el componente funciona a veces y a veces no”.

- Muchos de los errores más difíciles en React no se deben a código incorrecto, sino a expectativas incorrectas sobre cómo y cuándo React actualiza el estado.

- Aceptar que el estado puede estar en incertidumbre —que no es inmediato, que puede estar desfasado, que otros efectos lo afectan— te permite salir del ciclo de frustración y pasar al modo detective.

### Consejo final

La incertidumbre no siempre es un bug. A veces es una señal de que hay una desincronización entre tu lógica y el ciclo de vida de React.
