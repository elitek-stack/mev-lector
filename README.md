# Movimiento es vida · lector

Lector público (solo lectura) de la historia «Movimiento es vida» (Puerto Gris), basada en https://elitek-stack.github.io/MEV/.

Muestra únicamente la prosa que publica el Director a través del endpoint público `public_story` (slug `movimiento-es-vida-e89c545a`). Página estática, sin dependencias y sin secretos. Se actualiza sola cada 5 s mientras la pestaña está visible.

## Narrador

Botón 🔈 «Escuchar» en la cabecera: lee la hoja actual en voz alta con la Web Speech API (`speechSynthesis`), sin servidores ni librerías. Barra mínima: párrafo anterior/siguiente, play/pausa, velocidad (0.8×–1.6×) y detener. Resalta y desplaza al párrafo leído; tocar un párrafo salta a él. Al acabar la hoja pasa a la siguiente («Continuar al siguiente capítulo», en Ajustes, activado por defecto); al final dice «Fin de los capítulos publicados». Voz (solo es-*, por defecto la mejor disponible), velocidad y el interruptor se guardan con las preferencias; el progreso guarda el párrafo narrado. Las escenas nuevas o editadas no interrumpen la narración.

Soluciones a limitaciones conocidas (best effort, el audio real depende del navegador/SO):
- Chrome corta utterances largos: el texto se limpia y se trocea por frases (≤200 caracteres); en Chrome de escritorio, keep-alive con `pause()/resume()` cada 10 s; watchdog que reintenta o avanza si el motor se cuelga sin `onend`; hasta 2 reintentos por error.
- Pausa = cancelar y retomar el trozo actual (la pausa nativa falla en Android).
- Hace falta un gesto del usuario para empezar (botón Escuchar o ▶).
- iOS puede pausar la síntesis al bloquear la pantalla o pasar a segundo plano: al volver a la página se reanuda sola el trozo actual. Para escuchar en el carro, mejor con la pantalla encendida.
- Media Session (`navigator.mediaSession`): título del capítulo y controles play/pausa/siguiente/anterior párrafo; se reproduce un audio silencioso en bucle para que Android/iOS muestren esos controles (puede no aparecer en todos los dispositivos).
- Si el navegador no soporta `speechSynthesis` el botón no aparece; si no hay voces en español, la barra lo avisa.
