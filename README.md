# Easy Math Notes Web

![show_case_1](/screenshots/img0.png)

Sitio: [Easy Math Notes Web](https://jason-devcode.github.io/easy-math-notes-web/)

Sitio web que permite reconocer y convertir símbolos matemáticos manuscritos en LaTeX, usando un modelo de clasificación entrenado con el dataset HASYv2 y ejecutado íntegramente en el navegador con ONNX Runtime Web.

## ¿Con qué propósito se hizo?
El propósito de Easy Math Notes Web es resolver el problema de que, después de tomar apuntes matemáticos a mano, se pierde mucho tiempo transcribiendo y formateando todo a LaTeX para que quede formal.
La idea es permitir escribir las fórmulas directamente a mano en un canvas y que se conviertan automáticamente en tiempo real a código LaTeX de forma tan ligera que se ejecute dentro del navegador.

## Detalles Técnicos de la Solución

- Entrenamiento en Python/TensorFlow con HASYv2 (369 clases, 45×45 px, escala de grises).
- Exportación a ONNX (`math_symbols.onnx`).
- Carga al browser (WASM) y clasificación de crops de canvas.
- Salida: top-n sugerencias LaTeX (por ejemplo `\sum`, `\pi`, `+`, `=`).
- Fine-Tuning: Permite realizar correcciones de las salidas del modelo y exportarlas en formato JSON.
- [Repositorio de Entrenamiento](https://github.com/jason-devcode/EasyMathTraining)

## ¿Qué hace el sitio?

- Dibuja en un canvas y el sistema detecta componentes conectados.
- Cada símbolo recortado se reescala a 45×45.
- Se aplica la misma normalización/inversión usada en entrenamiento (trazo=1, fondo=0).
- Se envía a ONNX Runtime Web.
- Devuelve la clase con mayor probabilidad y top3 alternativas.
- Se puede usar para ensamblar expresiones completas en LaTeX con JS adicional.

## Guía rápida de uso

1. Accede a [Easy Math Notes Web](https://jason-devcode.github.io/easy-math-notes-web/).
2. Dibuja un símbolo.
3. El frontend segmenta y clasifica.
4. Se muestra el símbolo LaTeX detectado.

## Notas adicionales

- De momento no interpreta expresiones completas, solo símbolos aislados.
- Asegurar que la inversión de píxeles sea consistente entre entrenamiento e inferencia.
- ONNX Runtime Web es la opción elegida por rendimiento y tamaño.
