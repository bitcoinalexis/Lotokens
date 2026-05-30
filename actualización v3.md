CLAUDE.md bloqueado:
  - No puedo guardar tus preferencias de LoTokens ni de otras skills
  (update-config, init, etc.) de forma persistente.
  - No puedo añadir/editar instrucciones del proyecto que tú me pidas recordar
  ("de ahora en adelante haz X").
  - Comandos como /init fallan.
  
  MEMORY.md (y memory/*.md) bloqueado:
  - Se rompe el sistema de auto-memory: no puedo guardar nada sobre ti (rol,
  feedback, contexto de proyecto, referencias externas). 
  - Cada sesión empieza en frío — pierdes la continuidad entre conversaciones.
  - Si me pides explícitamente "recuerda esto", no podré cumplirlo.

  En resumen: bloquearlos te ahorra cero tokens (son escrituras puntuales, no
  repetitivas) y rompe la persistencia entre sesiones. La skill ya exceptúa
  CLAUDE.md; tiene sentido exceptuar también MEMORY.md y el directorio memory/.
