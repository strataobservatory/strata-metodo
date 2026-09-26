# Método de observación · Strata Observatory · versión 8.2

**Qué es este documento.** La descripción completa de cómo observamos, escrita para quien **no se fía de nosotros**. Se sella junto a cada observación que produce, de modo que dentro de diez años se pueda saber no sólo qué medimos sino **cómo lo medimos entonces**.

**Qué no es.** No argumenta que lo que medimos importe. No recomienda nada ni puntúa a nadie. Y no describe cómo se fecha el archivo: eso está en el procedimiento de verificación, que se publica aparte y funciona sin acceso a nuestros datos.

**Alcance de esta versión.** Cubre la **Capa 0 (censo)**, y sólo lo que se ejecuta. Las afirmaciones —Capa 1— y las sondas de comportamiento —Capa 2— **no están implementadas y no se describen aquí**: prometer un método que no se ejecuta sería exactamente lo que este proyecto no hace. Su diseño está en un documento aparte, que no se sella, no viaja en las copias y no es este método.

**Quién lo mantiene.** Strata Observatory, mantenido por Luis Calvo Ruiz. Sus datos de contacto al día están en https://github.com/strataobservatory. Aquí se nombra a quién y se apunta a dónde mirar, pero no se escribe ningún correo ni identificador: esos datos cambian, y este texto, una vez sellado, no.

---

## 1. El universo observado

Tres clases de objeto, que son el mismo ecosistema visto a tres niveles:

1. **Registros y directorios.** Los sitios que listan a los demás.
2. **Servicios listados en ellos.** El grueso de la población.
3. **Servicios y agentes con ficha propia en su dominio**, hallados sondeando rutas estándar sobre dominios ya conocidos.

**Ámbito: global.** No hay eje geográfico —estos objetos no tienen nacionalidad— ni filtro de idioma.

### La regla de inclusión

Un objeto entra en el censo si aparece en alguna de estas fuentes:

- **Listas enumerables** — las cuatro nombradas más abajo, y sólo ésas. Una quinta consta como declarada y aún no incorporada, sin estado de cobertura.
- **Rastro de dependencia**, hasta **dos niveles** desde un objeto ya censado. Al segundo nivel sólo entra lo que pertenece a las clases de arriba, no toda dependencia transitiva. **No se ejecuta**: se intentó una vez, el 2026-09-02, y no dio ningún objeto, porque su fuente es el repositorio de paquetes, que no se lee.
- **Frontera**: sondeo de rutas estándar sobre dominios conocidos, y vigilancia **filtrada por patrón de nombre** de los registros públicos de certificados. **La pasada diaria no la ejecuta.** El sondeo se hizo una sola vez, el 2026-09-02, y halló 34 servicios con ficha propia en 23 dominios. La vigilancia de los registros de certificados **no se ha hecho nunca**: su señal de exclusión nos la prohíbe desde el primer día.

**Ese filtro es parte de la frontera del universo**, no un detalle de implementación: lo que queda fuera del patrón consta como fuera de la regla de inclusión, **no como inexistente**.

**Qué se ejecuta cada día.** De los tres mecanismos de arriba, **sólo las listas enumerables se recorren en cada pasada**. A los 34 servicios que halló la frontera se les mira cada día en su propia dirección, una petición cada uno, pero **no se ha sondeado ningún dominio más**. Así que desde el 2026-09-02 **el universo sólo crece por las listas**, y lo que la frontera habría hallado después no está. Hasta la versión 7 esto no se decía, y la regla de inclusión ejecutada que se guardaba en el archivo seguía describiendo el barrido de aquel día. Desde la 8, la pasada la reescribe cada día con lo que se hizo ese día. Volver a ejecutar la frontera, y cada cuánto, sería cambiar lo que se observa: una versión nueva, con su discontinuidad.

### Las listas enumerables, nombradas

La versión 1 decía «registros y directorios públicos» sin nombrar ninguno, y esa vaguedad tuvo una consecuencia medible: se implementaron dos fuentes, y las otras tres **no quedaron excluidas: quedaron ausentes** — sin aparecer siquiera entre los descartes, de modo que nadie podía notar que faltaban. Un universo que no se nombra no se puede auditar.

Se recorren en este orden:

| Orden | Fuente | Identificador en el código |
|---|---|---|
| 1 | Registro oficial del protocolo | `registro-oficial-mcp` |
| 2 | Directorio Smithery | `directorio-smithery` |
| 3 | Directorio Glama | `directorio-glama` |
| 4 | Directorio PulseMCP | `directorio-pulsemcp` |

**La columna del identificador no es decorativa.** Es lo que permite comprobar a máquina que el método y el instrumento dicen lo mismo: si esta tabla nombra una fuente que el censo no intenta, o el censo intenta una que esta tabla no nombra, la verificación falla. El defecto que motivó esta versión queda así convertido en barrera.

Añadir o quitar una fuente de esta tabla es **cambiar el universo observado**, y por tanto una modificación del método con su entrada en el historial — nunca un cambio de configuración.

### Una fuente declarada que aún no se incorpora

Hay una quinta fuente que el proyecto decidió observar y que todavía no se lee. **No está en la tabla de arriba y no lleva estado de cobertura**: los tres estados de una fuente describen un intento, y con ella no se intenta nada. Tampoco se calla: consta aquí, con el día desde el que consta así y por qué, y se enseña en el histórico y en el cuadro.

| Fuente | Desde | Por qué no se incorpora todavía |
|---|---|---|
| `repositorio-npm` | 2026-09-17 | se sabe qué permite —sus condiciones permiten replicar el registro público por sus interfaces—, pero no hay todavía un recorrido determinista: su búsqueda devuelve como mucho 5.000 resultados, en un orden que se mueve, y la consulta por la palabra clave declara 72.182. Leerla así sería leer por posición, el defecto que ya retiró dos lecturas. Hasta la versión 7 constaba cada día `ilegible`, y no lo era: sí se sabía qué permite |

Incorporarla será, como cualquier cambio de la tabla de arriba, una versión nueva del método, y el día que entre será una discontinuidad declarada sobre esa fuente.

### Cada fuente consta con su resultado, y son tres distintos

De cada pasada, toda fuente de la tabla queda registrada en uno de estos estados. **Ninguna puede omitirse en silencio.**

| Estado | Qué significa |
|---|---|
| **Enumerada** | Se recorrió entera, o se dice dónde se cortó |
| **Excluida** | Sus señales de exclusión prohíben la superficie enumerable. Se registra y se para |
| **Ilegible** | No se pudo saber qué permite. No saber si está permitido no es permiso |

**«No se intentó» y «no nos dejaron» son cosas distintas y no pueden producir el mismo informe.** La primera habla de nosotros; la segunda, del sitio. Confundirlas convertiría un olvido propio en una negativa ajena, que es una afirmación falsa sobre un tercero.

**Este censo no aspira a ser completo. Aspira a ser profundo y consistente.** No se puede enumerar lo que no se sabe que existe, y decir lo contrario sería la primera mentira del archivo.

---

## 2. Cómo se observa

**El agente se identifica siempre**, en la cabecera de cada petición, con su nombre —`strata-observatory`—, la dirección de la página del proyecto, que enlaza en un paso a donde se publican todas las versiones de este documento, y su correo de contacto. Un registro construido escondiéndose no atestigua nada.

**Sólo superficie pública, en sentido estricto**: accesible sin credenciales ajenas, sin rodear ningún control y sin aceptar condiciones que lo prohíban.

**Las señales de exclusión del sitio se respetan como norma absoluta.** Lo que no se pueda observar así consta como **no observable por política** y permanece en el censo con su motivo.

**Y las señales de USO declaradas también se respetan.** Algunos sitios declaran en su `robots.txt`, junto a las exclusiones, cómo permiten que se consuma su contenido —búsqueda, entrada a modelos, entrenamiento, y con qué alcance—. **Nuestro uso es de referencia y archivo: se guarda lo que el objeto declara de sí mismo para poder decir después qué decía y cuándo. No se entrena nada con ello, y no se redistribuye el contenido ajeno.** La señal concreta de cada sitio no se copia aquí: se registra **en cada pasada**, con su fecha, porque es una declaración del observado y puede cambiar cualquier día — y una frase de un tercero congelada dentro de nuestra doctrina dejaría de ser suya. Que no la declaren no es permiso ni prohibición, y así consta.

**Carga cero sobre el observado.** Se pregunta si algo ha cambiado antes de descargarlo: se guarda el hash en cada pasada y el contenido **sólo cuando el hash cambia**.

**Si un objeto bloquea el acceso, se registra el bloqueo y se para. No se rodea.** El bloqueo es un dato en sí mismo.

**Quien no quiera ser observado puede pararnos, y la vía es su propio `robots.txt`.** Si nombra a nuestro agente, se respeta como cualquier exclusión en la pasada siguiente, sin que nadie de nuestro lado tenga que leer nada. El nombre se reconoce como lo escribiría quien lo ha visto en su registro de accesos: con o sin versión, con la cabecera entera pegada, con mayúsculas o separadores distintos.

**Para quien no pueda tocar su `robots.txt`, la alternativa es una petición escrita**, al correo del proyecto o abriendo una incidencia en su página. **Se cumple como mucho cinco días después de que llegue**, y ése es el plazo que se cumple en el peor mes, no en uno normal. Quien mantiene el observatorio mira el correo y las incidencias al menos cada tres días, y cada vez que mira queda escrito el día, aunque no hubiera nada. Cada petición pendiente queda escrita también, con el día en que llegó. **El vigía avisa**, igual que avisa de un día que falta: si pasan más de tres días sin mirar, si una petición pasa del plazo, o si una incidencia sigue abierta más que él. Cumplirla es añadir la dirección —un dominio, o una ruta dentro de un sitio, como una cuenta en un sitio de alojamiento— a una **lista declarada** que viaja con el código del instrumento, y contestar a quien la hizo. La lista lleva la dirección, el día en que llegó la petición y por dónde llegó; **nunca quién la hizo**.

**La lista se lee al empezar cada pasada, antes de cualquier fuente**, y si no se puede leer, la pasada no empieza: no saber a quién no hay que mirar no es permiso para mirar a todos. Lo que cubre **no recibe ninguna petición** —tampoco la de su `robots.txt`— **y no se apunta nada de ello**: ni altas, ni hechos, ni ausencias. Cada día consta **no observable por política**, con el motivo y el día en que llegó la petición, sin la dirección. La serie se cierra con ese motivo, nunca con un hueco. **Y cada día se sella, en su cobertura y sin nombres, cuántas direcciones están excluidas a petición**: sin ese número, la cobertura de un día podría ser más estrecha que la del anterior sin que se viera por qué. Lo sellado antes no se borra, porque ningún día se resella.

**Nunca se observa nada tras credenciales de otro.** El instrumento no sabe mandarlas, y un rechazo es un bloqueo (arriba).

**De cada objeto se guarda lo que él mismo o la fuente que lo lista publican sobre él**: su nombre en esa fuente, la dirección pública donde está publicado —tal como la publican las fuentes—, los atributos que declara y el hash de su declaración. Esa dirección es a veces la de un repositorio bajo la cuenta de una persona, porque así nombran las cosas los sitios de alojamiento: el objeto es el repositorio, no la cuenta. **No se vinculan objetos por su propietario**: no se agrupan, no se cuentan y no se deriva nada por cuenta, autor, mantenedor ni organización. Y a quien sea dueño de una de esas direcciones le vale lo de arriba: puede pedir salir.

**Nada entra en el censo por otra puerta que las fuentes nombradas en el apartado 1.** La pasada se niega a dar de alta desde cualquier otra, y el verificador comprueba en cada día sellado que cada alta viene de una de ellas. Por eso nada llega por la relación de quien mantiene el observatorio con sus clientes, ni por ninguna otra vía.

---

## 3. Los estados de cobertura

Cada objeto, cada día, consta en uno de estos estados. **La cobertura es un dato de primera clase**: un hueco registrado es información, y un hueco callado sería una mentira que contaminaría el archivo entero.

| Estado | Qué significa |
|---|---|
| **Observado** | Se miró y se obtuvo respuesta |
| **No observado** | No se miró. Consta el motivo |
| **Fallo del observado** | Se miró y el objeto no respondió correctamente |
| **Bloqueado** | El objeto rechazó el acceso |
| **No observable por política** | Podría mirarse técnicamente, pero hacerlo incumpliría el apartado 2 |

Un periodo sin registro de cobertura no existe: si no consta, el archivo está incompleto y la verificación lo dice.
**Un objeto que falta de una lista recorrida entera consta `observado`, con su motivo**, y no en un sexto estado: se miró y no estaba, que no es lo mismo que no haberlo mirado. Lo que se hace con esa ausencia está en el apartado 10.
**Y el estado de cada FUENTE cada día es parte del archivo sellado.** No es lo mismo que lo de arriba: aquello habla de un objeto, esto de una lista entera, y consta como *enumerada*, *excluida* o *ilegible*, nunca omitida en silencio (apartado 1). Va dentro del sello **porque es la evidencia de la que depende toda afirmación de nacimiento**: un objeto consta como nacido bajo observación porque la fuente que lo trae se recorrió entera el día anterior, y quien no pueda comprobar esa fila no puede comprobar el nacimiento. Un archivo que afirme lo segundo sin sellar lo primero está afirmando algo que no respalda.
**Un día que no se observó no lleva filas de fuente. Ninguna.** Si la pasada de un día no ocurre, ese día no se mide después —sería grabar el estado de hoy como si fuera el de entonces—: se sella como no observado, con cada objeto en *no observado* y su motivo, y **sin ninguna fila de fuente**. Las tres respuestas de una fuente describen un intento, y ese día no lo hubo; lo que pasó le pasó al día, no a las fuentes. Y la cabecera del día **lo dice**: `no_se_corrio` si la pasada no ocurrió, y entonces no hay ninguna fila; `corrio_sin_observar` si se intentó y no se pudo observar nada, y entonces cada fuente lleva su fila y ninguna consta *enumerada*. La distinción vive en un valor dicho, no en un hueco. No es un cuarto estado de fuente: el vocabulario cerrado es el de la fuente, y éste es el del día. **Un día perdido cuesta un día**: la pasada siguiente lo sella antes que el suyo, porque la cadena no admite huecos.

---

## 4. Qué se registra de cada objeto

**Un identificador propio**, asignado la primera vez y **nunca reutilizado**. Los nombres externos son alias con su fecha.

**Sus atributos**, que viven en el objeto y no se repiten en cada observación: clase, proveedor u organización responsable, tipo o dominio funcional declarado, protocolo y superficie técnica, alojamiento, licencia, procedencia, fuente que lo descubrió, objeto padre si vino por dependencia, y si **nació bajo observación** o ya existía cuando llegamos.

Los atributos **son series dispersas, no campos que se sobrescriben**: casi ninguno cambia nunca, y cuando uno cambia se añade una entrada con su fecha de validez. Sin eso no se podría preguntar cómo se comportaban en 2027 los objetos de un tipo, porque haría falta saber de qué tipo eran *entonces*.

**Lo que el objeto declara y lo que nosotros clasificamos se guardan separados y marcados.** Lo primero es una medición; lo segundo, una interpretación — y nuestra clasificación lleva su propia versión de método.

**El hash de la declaración completa**, cada día. El contenido, sólo cuando el hash cambia.

---

## 5. Cuándo dos observaciones son del mismo objeto

Importa más de lo que parece: si un cambio de nombre se registra como una muerte y un nacimiento, la mortalidad que publicamos sería falsa.

**Hoy un objeto se reconoce por su nombre en la fuente, y no se funde ninguno.** El mismo nombre, venga de la lista que venga, es el mismo objeto, y cada lista que lo trae le suma un avistamiento. Pero cada directorio nombra con su propio espacio de nombres —el registro oficial `io.github.x/y`, Smithery `x/y`, PulseMCP `x-y`—, así que en la práctica ningún objeto tiene avistamientos en más de una lista: **un servicio listado en cuatro directorios son cuatro objetos** (apartado 10).

**Lo único que se graba entre listas es una nota de vínculo sospechado.** Al dar de alta un objeto, si otro de otra lista tiene el mismo nombre una vez quitado el prefijo de cada directorio, se anota la relación posible con esa evidencia. La nota no funde nada: permite reunirlos después.

> **Separar es recuperable; fusionar no.** Unir con evidencia débil deja de contar muertes y hace que la supervivencia salga optimista. Separar de más sobrestima algo la mortalidad, y la nota de vínculo permite reunirlas después. **Se asume ese sesgo pesimista a conciencia, y se dice.**

**Un objeto que cambia de nombre** consta como una ficha que deja de estar y otra que aparece, con nota sólo si sus nombres coinciden como arriba. Eso sobrestima la mortalidad de fichas, y se asume.

**Nunca se une por propietario** (apartado 2): la cuenta, el autor o el mantenedor no son evidencia de identidad, y no se usan para nada.

Cada decisión de identidad se graba con su evidencia. Revisarla es añadir una entrada, nunca reescribir.

**Una escalera que funda con evidencia declarada o estructural está diseñada y no está conectada.** Su diseño está en el documento aparte del alcance. Conectarla cambiaría lo que se cuenta, así que será otra versión, y una discontinuidad.

La otra mitad de esto —cuándo un objeto deja de estar, y por qué eso no es lo mismo que una muerte— está en el **apartado 10**.

---

## 10. Ausencia y muerte

**Por qué este apartado lleva el número 10 y va aquí.** Porque los números de apartado **no se corren**. Los cierres del archivo y los comentarios del instrumento citan «apartado 5» o «apartado 8», y esas citas tienen que seguir significando lo mismo dentro de diez años. Es la misma regla que gobierna los identificadores propios del censo —el contador sólo sube, ni siquiera tras una muerte— y la misma que prohíbe reetiquetar una observación sellada. Va colocado detrás del apartado 5 porque es su continuación natural: aquél decide cuándo dos observaciones son del mismo objeto, y éste cuándo un objeto deja de estar.

Este apartado es **el espejo de la regla de nacimiento**, y hasta la versión 4 no existía. El método hablaba de mortalidad y de supervivencia en cinco sitios y el instrumento sólo marcaba una baja cuando una identidad se partía en dos: un objeto que dejaba de aparecer en una lista recorrida entera no se registraba en ninguna parte.

### Las tres puertas

Un objeto **falta** un día si se cumplen las tres:

1. la fuente que lo listaba se recorrió **entera y sin corte** ese día —enumerada, y sin corte declarado—;
2. el objeto no aparece en ese recorrido;
3. y eso vale para **todas** las fuentes que lo listaban.

La tercera es la que el nacimiento no necesita y ésta sí: un objeto puede estar en cuatro directorios y desaparecer de uno. **Si alguna de sus fuentes no se recorrió entera, no falta** — no llegamos a mirar, que es distinto de mirar y no encontrar. Una fuente cortada no puede matar a nadie.

### Ausencia y muerte son dos cosas distintas

| | cuándo | qué es |
|---|---|---|
| **Ausente** | desde el **primer** día que falta | un hecho **reversible**, que se graba y se puede deshacer |
| **Reaparecido** | si vuelve | **un dato, no un borrado**: mide cuánto ruido tiene la fuente |
| **Baja** | tras **N** días ausente | y **fechada en el primer día de ausencia**, no en el enésimo |

Que la muerte se **retrofeche al primer día de ausencia** es lo que hace funcionar todo lo demás: el archivo es un instrumento de fechas, y la fecha en que algo dejó de estar es el día en que dejó de estar, no el día en que nosotros nos convencimos.

**Se cuentan dos plazos, no uno.** Un día en que la fuente no se pudo recorrer entera no confirma la ausencia ni la desmiente: no cierra el episodio —no es una reaparición— pero tampoco cuenta. Por eso cada episodio lleva sus **días de calendario** y sus **días confirmados**, y son distintos.

### N no está fijado, y se dice

**`N` no tiene valor en esta versión, y ninguna muerte se declara por ausencia.** Un número elegido por criterio se mide antes de aceptarlo, y `N` no se puede medir sin saber cuántas ausencias revierten. La primera medición, sobre los cinco primeros días del archivo, dice por qué no puede ser 1: **270 episodios, de los que 156 ya se cerraron y los 156 reaparecieron al día siguiente.**

Y no hace falta correr. **Como la muerte se retrofecha, no se pierde nada esperando**: si `N` se fija dentro de tres semanas, las muertes salen con su fecha correcta igual. Lo único que no se puede recuperar es no haber empezado a grabar.

### Qué se mide: fichas listadas, no servidores

Lo que esta regla mide no es la mortalidad **de servidores**: es la mortalidad **de fichas listadas**. El apartado 5 no une las observaciones de dos directorios —ningún objeto del censo tiene avistamientos en más de una lista—, así que un mismo servicio listado en dos directorios son dos objetos. Si desaparece de uno y sigue en el otro, cuenta como una baja en el primero, y **está bien que cuente**: su ficha allí dejó de estar. Por eso la frase que se publique tiene que decir lo que se mide:

> *«De las N fichas listadas en el registro oficial del protocolo el 2 de septiembre de 2026, el X % ya no aparecía treinta días después.»*

Menos alcance del que sonaría con «servidores», y la precisión que esa otra frase no tendría. **Y una consecuencia sobre la tercera puerta:** mientras cada objeto lo liste una sola lista, faltar en *todas* sus listas es faltar en la suya. La puerta queda escrita igual, y el día que se conecte una escalera que una dos directorios, actuará sola.

### Otras puertas de una fuente

Una fuente puede tener **más de una puerta**, y no tienen por qué decir lo mismo. El 2026-09-10 salieron 33 ausencias del directorio Smithery que no eran de nuestra lectura —su listado, recorrido entero dos veces, ya no las enumeraba— y que seguían existiendo: su búsqueda las encontraba. Faltar del listado y seguir en la búsqueda **no es lo mismo que faltar de todas partes**, y tiene estado propio.

Por eso, a cada ausencia confirmada de una fuente con otras puertas se le pregunta, ese mismo día, a cada una, y **cada respuesta se sella como una observación aparte**: *presente*, *ausente* o *no se pudo preguntar*, que es un resultado y no un hueco.

| Fuente | Otra puerta | Qué gobierna |
|---|---|---|
| `directorio-smithery` | la ficha, por el nombre exacto | la baja: es determinista |
| `directorio-smithery` | la búsqueda, por el nombre exacto | nada: se sella como observación |

**Manda la ficha.** El listado sigue midiendo la ausencia; la ficha, que responde lo mismo cada vez que se le pregunta, gobierna la baja; la búsqueda ordena por relevancia —*ausente* ahí sólo quiere decir que no apareció entre los primeros resultados para su nombre exacto— y habla de un reordenador, no del objeto. Se guarda porque es un dato, y no decide nada. Una baja, cuando exista, **exigirá silencio en la ficha**.

### La cuarentena de lo que no tiene precedente

**Se retiene la consecuencia, nunca la inscripción.** Lo observado se sella siempre. Lo que se frena es lo que se **deduce** de ello —las ausencias que entran un día, las reapariciones de un día— cuando no tiene precedente: si el valor del día supera **a la vez** un múltiplo declarado del mayor valor anterior ya consumido de esa magnitud **y** un suelo absoluto declarado para ella, todo lo de esa magnitud ese día se sella **en cuarentena**. Queda en el archivo, con la cifra que lo disparó y el listón contra el que se midió; pero **no se consume**: no entra en la serie, no cuenta como abierto y no se acerca a ninguna baja.

| Parámetro | Valor |
|---|---|
| Múltiplo del umbral de cuarentena | `3` |
| Suelo absoluto de `ausencias_entran` | `42` |
| Suelo absoluto de `reapariciones` | `4` |
| Serie de la que sale el suelo | del `2026-09-10` al `2026-09-14` |
| Plazo de la cuarentena | `14` días |

El umbral tiene **dos términos, y hay que pasar los dos**. El múltiplo es **relativo a la propia serie**, para que no haya que reajustarlo al crecer la población; lo retenido no cuenta para ese máximo: si contara, el primer disparate haría invisible al segundo. El suelo es **absoluto**, para que una serie todavía corta, o de ceros, no retenga el movimiento ordinario de un día: contra ceros, el múltiplo solo lo dispararía cualquier cifra.

**Cómo sale el suelo, sellado con él para que se pueda rehacer.** El suelo de cada magnitud es el mayor valor diario de esa magnitud en la serie limpia: los días de la serie comparable —desde el 2026-09-10, el primero en que las fuentes que se pueden leer se leyeron enteras con la lectura de hoy— hasta el 2026-09-14, el último sellado antes de fijarse, contando lo que existe: sin lo anulado por una retractación y sin lo retenido. Día a día, las ausencias que entran fueron 42, 14, 11, 13 y 9, y las reapariciones 0, 2, 4, 0 y 0. Así el suelo queda por encima del mayor movimiento diario ordinario de la serie limpia y muy por debajo del incidente del 2026-09-08 (11.710). Quien verifique el archivo desde fuera recuenta esa serie con lo sellado y comprueba que da estos suelos. Cambiar un suelo, o la serie de la que sale, es una versión nueva del método.

**Sale de cuarentena de dos maneras, y las dos se sellan**, una entrada por objeto: **levantada**, cuando una persona decide que la cifra es del mundo y no del instrumento; o **caducada**, cuando pasa el plazo sin decisión —y entonces cuenta, con la marca de que nunca se resolvió, y el día que caduca se avisa como el día que se abrió—. Si lo que se decide es que la cifra era falsa, no se levanta: se retracta, entrada por entrada (apartado 8). Cuánto se tardó en resolver una cuarentena es a su vez un dato sobre el instrumento.

**Las bajas** también son una magnitud derivada, y entrarán aquí cuando existan; hoy no hay ninguna, porque `N` no está fijado.

### Hacia dónde falla esta regla

**Hacia «no ha muerto».** Un nacimiento no declarado empobrece una cohorte nuestra; una muerte falsa es **una afirmación falsa sobre un tercero**: decir que algo dejó de existir cuando existe. Es la misma familia que «no se intentó» frente a «no nos dejaron», y en esa familia este método elige siempre el mismo lado.

Consecuencia declarada, como la sobrecuenta del apartado 7: **la mortalidad que se publique será una cota inferior.** Se dice, no se disimula.

### Qué se sella, y qué estado de cobertura le toca

**Cada día confirmado de ausencia va dentro del sello**, atado al día en que empezó su episodio, y también la reaparición que lo cierra. Va dentro por lo mismo que el estado de cada fuente entró en la versión 4: es la evidencia de la que dependerá toda afirmación de mortalidad, y quien no pueda recontarla no puede comprobar la afirmación. Se sellan **todos** los días confirmados y no sólo el primero, porque lo que hay que poder recontar es cuántos días se confirmó, no cuántos pasaron.

**Un objeto ausente sigue constando `observado`**, con su motivo escrito. No hay un sexto estado de cobertura: los cinco del apartado 3 contestan *«¿conseguimos mirarlo?»*, y aquí se miró —se recorrió la lista entera—. *«¿Estaba?»* es otra pregunta, con otra forma —un intervalo, no el estado de un día—, y por eso se registra aparte. Meterlas en la misma columna sería repetir el error que el apartado 1 ya prohíbe expresamente: confundir «no nos dejaron mirar» con «miramos y no estaba».

---

## 7. Qué no está medido

Dicho entero, porque es lo que hace citable el resto.

- **El comportamiento real no se mide en esta versión.** Todo lo anterior compara lo declarado contra lo declarado antes. Que un servicio haga lo que dice **no se comprueba**: eso es la Capa 2 y no existe.
- **El censo no es completo.** Sólo alcanza lo que las fuentes del apartado 1 exponen, dentro del filtro declarado.
- **Un objeto puede cambiar y volver** entre dos observaciones diarias sin que lo veamos. La resolución es la cadencia.
- **De la población del primer día no se sabe cuándo nació, y no se sabrá nunca.** Que un objeto naciera bajo observación se afirma comparando la lista de hoy con la de ayer, no creyendo la fecha que el objeto declare —esa no se puede validar—. El primer día no hay ayer contra el que comparar, así que **todo lo censado ese día consta como ya existente** y queda fuera de cualquier cohorte de nacimiento para siempre. Sólo lo que aparece a partir del segundo día tiene una vida entera medible. Y **«entera ayer» quiere decir entera ayer con la misma lectura**: el día de una discontinuidad declarada sobre una fuente, ninguna de las altas que trae esa fuente es un nacimiento —su motivo es la discontinuidad—, porque lo que ese día aparece puede ser sólo lo que empezamos a ver. La fracción de la población que está en cada caso se publica con la serie.
- **No sabemos por qué cambió nada.** Registramos que cambió y cuándo.
- **Lo no observable por política puede estar cambiando** todo el tiempo, y consta que no lo miramos.
- **Nuestra clasificación es una interpretación nuestra**, no un hecho sobre el objeto, y va marcada como tal.

---

## 8. Versionado de este método

**Cada observación graba la versión del procedimiento que la produjo, y el texto del procedimiento se sella junto a los datos.** Un número de versión sin el texto que describía no prueba nada.

El test que separa las dos clases de cambio:

> **Si volviendo a medir lo de ayer el resultado pudiera salir distinto, es una discontinuidad. Si no, es una versión compatible.**

En una discontinuidad se solapan ambos procedimientos mientras sea posible, para dejar un puente de calibración; cuando el objeto ha cambiado de forma que el procedimiento antiguo ya no se puede ejecutar, se declara el corte y consta. Saltarse el solape es admisible **con excusa escrita**, nunca en silencio.

Una discontinuidad puede declararse **sobre una serie** y no sólo sobre un procedimiento, para el caso en que nadie toque el método pero el objeto cambie de forma que lo mismo pase a medir algo distinto.

**Las discontinuidades declaradas sobre una fuente**, con su día. Es la tabla que lee la regla del nacimiento —ese día, las altas de esa fuente no son nacimientos— y la que comprueba quien verifique el archivo desde fuera:

| Día | Fuente | Qué cambió en su lectura |
|---|---|---|
| 2026-09-08 | `directorio-pulsemcp` | se lee por el conjunto que declara su sitemap, no recorriendo su paginación |
| 2026-09-08 | `directorio-smithery` | se lee con una semilla que fija el orden, no por un orden que se mueve |

**Nunca hacia atrás**: ni se reejecuta un método nuevo sobre datos viejos haciéndolos pasar por originales, ni se reetiquetan observaciones ya selladas. Un error se corrige **añadiendo** una entrada de corrección con su fecha, y el original queda intacto.

**Un error sistemático se retracta entrada por entrada.** Cuando un defecto del instrumento produce muchas afirmaciones falsas a la vez, cada una lleva su propia corrección, con el día y el identificador de la entrada que retracta: son afirmaciones sobre terceros con nombre, y cada uno merece su retractación con su nombre. Una corrección colectiva no existe en el formato, y no se inventa bajo la presión de un error. **Se sella el día en que se decide**, no el día en que el defecto se cerraría solo. Y **el orden es obligatorio: primero se sella la corrección, y sólo después se mueve la base del censo**; al revés habría un rato en que la base niega lo que el sello afirma, y si el sellado fallara, ese rato sería para siempre. Lo retractado queda **anulado**, que no es lo mismo que **reaparecido**: un episodio que abrió un defecto nuestro no dice nada del mundo, y no entra en ninguna medida del ruido de una fuente. Así se retractaron, en el sello del 2026-09-09, 11.652 ausencias falsas del 2026-09-08.

---

*Este método es público desde el 2026-09-15, con todas sus versiones. El archivo que produce, no. La razón es que el método es replicable y el histórico no lo es: publicarlo no regala nada, y a cambio permite que alguien desconfíe de nosotros y aun así pueda aceptar el dato.*

---

## 9. Historial de versiones de este método

| Versión | Qué cambió | Por qué |
|---|---|---|
| 8.2 | **correcciones**: el día pasa a fecharlo un sello de tiempo de dos autoridades independientes en vez del alojamiento del testigo, que se queda probando qué se publicó y en qué orden; con la obligación fechada de volver a sellar antes de que caduquen sus cadenas (2037 y 2040) | la capa que fechaba compartía proveedor con el repositorio testigo y con el vigía —tres capas que sólo valen si fallan por separado no pueden depender del mismo sitio— y además **sólo la podíamos comprobar nosotros**: un testimonio que el lector no puede verificar por su cuenta es indistinguible de uno inventado |
| 8.1 | **correcciones**: se declara la discontinuidad de la capa institucional —hasta el 2026-09-20 en el banco de pruebas, con identificadores que no son permanentes; desde el 2026-09-21 en el registro permanente— | los recibos de antes y de después del 2026-09-21 apuntan a servicios distintos, y quien los comparase sin esto no sabría por qué. Un identificador `10.5072` no es citable: decirlo es parte de no prometer más de lo que se tiene |
| 8 | **apartado 1**: el repositorio de paquetes sale de la tabla de fuentes con estado de cobertura y consta como **fuente declarada aún no incorporada**, con el día y el motivo; y se dice qué mecanismos de la regla de inclusión se ejecutan cada día y cuáles se ejecutaron una sola vez. **Alcance**: sólo la Capa 0, y **se quita el apartado 6** (afirmaciones), cuyo diseño pasa a un documento que no se sella. **Apartado 2**: se deja de observar a quien lo pida, por su `robots.txt` o por correo, con una lista declarada que la pasada lee antes de cualquier fuente, un plazo publicado de cinco días con rastro y aviso, y la cuenta diaria, sin nombres, de lo excluido; se dice qué se guarda de cada objeto y que no se vincula nada por propietario, y que nada entra por otra puerta que las fuentes nombradas. **Apartado 5**: lo que de verdad hace la identidad —nombre por fuente, nota de vínculo sospechado, ninguna fusión—. **Pie**: desde cuándo es público | constaba cada día `ilegible`, que no era cierto: se sabe qué permite. Lo que falta es un recorrido determinista, y eso no es un estado de la fuente sino una decisión nuestra. Y la regla de inclusión describía tres mecanismos cuando la pasada diaria ejecuta uno: los otros dos sólo corrieron el 2026-09-02. Y repasado todo lo que el método declaraba, cinco frases más describían algo que no ocurría: la Capa 1, dejar de observar a quien lo pida, el enlace a este documento, que el método fuera público y la escalera de identidad. Y quien pidiera no ser observado no tenía cómo, mientras la página del proyecto lo ofrecía. Y la única vía que sí paraba al agente, un `robots.txt` que lo nombrara, sólo lo paraba con el nombre escrito exactamente así: con versión u otra capitalización no, y quien lo intentara no se enteraba |
| 7 | **apartado 3**: un día que no se observó se sella sin filas de fuente y lo dice en su cabecera (`no_se_corrio` o `corrio_sin_observar`), y un día perdido lo sella la pasada siguiente. **Apartado 8**: un error sistemático se retracta entrada por entrada, se sella el día que se decide y la base se mueve después del sello. **Apartado 7**: «entera ayer» quiere decir con la misma lectura, y el día de una discontinuidad declarada sobre una fuente sus altas no son nacimientos; **apartado 8**: la tabla de esas discontinuidades. **Apartado 10**: lo que se mide es la mortalidad de fichas listadas, no de servidores, entra la cuarentena de las magnitudes derivadas, y las otras puertas de una fuente se preguntan y se sellan. Y **apartado 9**: vuelve la fila de la versión 4, que se había perdido, y la tabla recupera su orden. Y el preámbulo dice quién mantiene el método y dónde están sus datos de contacto al día | un día perdido bloqueaba todos los siguientes, y la única recuperación sellaba ese día de una forma que el verificador rechazaba. El 2026-09-08 se sellaron 11.652 ausencias falsas: el método no decía cómo se retracta un error así, y nada impidió que 11.710 ausencias contra una serie de ceros se trataran como reales. Y la frase de la tasa tenía que quedar escrita antes de que haya una tasa |
| 6 | **apartado 2**: se declaran las señales de uso —que se respetan, y cuál es el nuestro—. **Apartado 1**: se corrige la tabla de fuentes, que traía dentro una fila del historial. Y una **discontinuidad**: PulseMCP pasa a leerse por el conjunto que declara su sitemap, en vez de recorriendo su paginación | leer por posición es inestable por definición: si la lista se mueve mientras se recorre, un objeto que retrocede se lee dos veces y otro que avanza no se lee nunca. Medido, eso producía **247 de las 270 ausencias** del archivo, 242 de ellas de un solo día. Un conjunto no tiene posición |
| 5 | **apartado 10 nuevo**: la regla de ausencia y muerte, con sus tres puertas, la separación entre ausencia y muerte, la retrofecha de la baja al primer día de ausencia y `N` explícitamente sin fijar. **Apartado 3**: un objeto que falta de una lista recorrida entera consta `observado` con motivo, y no en un sexto estado | el método hablaba de mortalidad y supervivencia en cinco apartados y el instrumento **no tenía la regla**: 49.720 objetos, 0 con día de baja, y la única baja posible era la de una identidad partida en dos. El nacimiento se hizo y su espejo se quedó sin hacer, y la supervivencia necesita los dos. Se escribe **antes de que haya ninguna muerte que contar**, para que la regla no la escriban los datos |
| 4 | **apartado 3**: el estado de cada fuente cada día pasa a ser parte del archivo sellado, y el verificador exige que cada día traiga la fila de todas las fuentes que el método de ese día nombra | ese dato es del que depende la regla de nacimiento del apartado 7, y vivía sólo en una base local: no se sellaba, ningún verificador lo miraba y no viajaba en la copia. El producto entero descansaba sobre el único trozo del censo que nadie podía comprobar |
| 3 | **apartado 7**: se dice que la población del primer día está cortada por la izquierda y no puede entrar en ninguna cohorte de nacimiento, y que el nacimiento se afirma con nuestra cobertura y no con la fecha que el objeto declare | la versión anterior no decía nada de esto, y el instrumento estaba clasificando como «nacido bajo observación» a quien lo **declaraba**: 474 objetos del primer barrido, ninguno visto aparecer. Dejar que una declaración —que no se puede validar— decida una clasificación nuestra es lo que el apartado 4 prohíbe |
| 2 | **apartado 1**: las cinco listas enumerables pasan a estar **nombradas**, con su orden de recorrido, y se añade la regla de que cada una consta como *enumerada*, *excluida* o *ilegible*, nunca omitida en silencio | la versión 1 decía «registros y directorios públicos» sin nombrarlos. El instrumento implementó dos de cinco y las otras tres quedaron **ausentes**, no excluidas: no aparecían ni en los resultados ni en los descartes. Un universo que no se nombra no se puede auditar |
| 1 | — | primera versión |

**La versión 8 no es una discontinuidad**, por el criterio del apartado 8: la fuente que sale de la tabla no aportó ni un objeto ningún día —constaba `ilegible`, con cero—, así que volver a medir cualquier día anterior sin ella daría el mismo resultado. Cambia lo que se afirma de ella, no lo que se mide.

**Retractación, decidida el 2026-09-15 y sellada con esta versión, de lo que el apartado 1 afirmaba desde la versión 4.** Del 2026-09-02 al 2026-09-15 —catorce días sellados, con las versiones 4, 5, 6 y 7— el apartado 1 decía que un objeto entra en el censo, además de por las listas, por el «rastro de dependencia, hasta dos niveles desde un objeto ya censado» y por la «frontera: sondeo de rutas estándar sobre dominios conocidos, y vigilancia filtrada por patrón de nombre de los registros públicos de certificados». En un texto que describe cómo se observa, eso afirma que esos mecanismos funcionan. **Era falso.** El rastro de dependencia se intentó una vez, el 2026-09-02, y no dio nada. El sondeo de rutas estándar se hizo una sola vez, ese mismo día. Y la vigilancia de los registros de certificados no se ha hecho nunca. Esos textos no se editan: siguen sellados tal como estaban, cada uno en sus días. Se retractan aquí, añadiendo y con fecha, como se retractaron las 11.652 ausencias falsas del 2026-09-08. Lo que se afirma desde esta versión es lo que dice ahora el apartado 1.

**Retractación, decidida el 2026-09-15 y sellada con esta versión, de cinco afirmaciones más de las versiones 4 a 7.** La de la frontera no era la única. Repasado todo lo que el método declaraba, y buscado cada mecanismo en el código y en los catorce días sellados —del 2026-09-02 al 2026-09-15—, había cinco frases más que describían algo que no ocurría:

- «Cubre la Capa 0 (censo) y la Capa 1 (afirmaciones)», y en el apartado 6, «las afirmaciones se derivan de la observación del censo y sólo se escriben cuando caen». **Era falso.** Ninguna pasada ha derivado nunca una afirmación, ni ha detectado que cayera: no hay código que lo haga, y en los catorce días sellados no hay ni una entrada de ese tipo.
- «Si alguien pide dejar de ser observado, se deja de observar y se registra la petición con su fecha». **No existía el procedimiento**: ni un registro de peticiones, ni nada en la pasada que las cumpla. No llegó ninguna petición, así que no se observó a nadie contra su voluntad; pero el texto describía un mecanismo que no había.
- «El agente se identifica siempre, con un enlace a este documento». Se identificó siempre. **El enlace, no**: hasta el 2026-09-14 apuntaba a una dirección bajo un dominio reservado, que no puede resolverse nunca, y el 2026-09-15 a la página del proyecto, que no enlaza a este documento.
- «Este método es público». **No lo era** en ninguno de los catorce días: su dirección pública se abrió el 2026-09-15 a las 08:32, hora de Madrid, después del sellado de ese día.
- En el apartado 5, «la continuidad se establece por escalera de evidencia», con una evidencia estructural de «mismo repositorio, misma identidad de paquete, mismo mantenedor, misma clave», y «un objeto listado en cuatro directorios es una identidad con cuatro avistamientos». **No era así.** Ningún peldaño que funda estaba conectado: ninguna fuente aporta evidencia declarada, y la búsqueda por identidad de paquete existe en el código pero no se llama. El repositorio se descartó a propósito —uno solo contiene 127 servidores, y los habría fundido en uno— y el mantenedor no se ha usado nunca. Lo que corría era otra cosa: una nota de vínculo sospechado por nombre, al dar de alta. Y un servicio en cuatro directorios son cuatro objetos, como ya reconocía el apartado 10 desde la versión 7.

Esos textos no se editan: siguen sellados tal como estaban. Se retractan aquí, añadiendo y con fecha, igual que la frontera. Lo que se afirma desde esta versión es lo que dicen ahora el alcance, los apartados 2 y 5 y el pie.

**El apartado 6 se quita, y los demás no se renumeran.** Describía la Capa 1, que no se ha ejecutado nunca. Marcarlo «no implementado» seguía metiendo en el documento de registro lo que no se hace, y así se acumularon estas frases. Su diseño pasa, con el de la escalera de identidad, a un documento aparte que no se sella, no viaja en las copias y no se llama método. Los demás apartados conservan su número, como el 10 conservó el suyo: los cierres y el instrumento los citan.

**La versión 7 no es una discontinuidad**, por el criterio del apartado 8: volver a medir lo de ayer no daría un resultado distinto. La cuarentena no cambia ninguna medida: cambia qué se consume de lo que se deduce. Y el resto de lo que añade describe cómo se sella un día que **no** se midió —y hasta hoy no se ha perdido ninguno—, cómo se retracta un error —y la retractación del 2026-09-09 ya se hizo así, con la versión 6— y qué significa la tasa que un día se publique. Ninguna medida cambia.

**Corrección de lo que hizo la capa institucional, declarada aquí porque el método viaja dentro de cada paquete.** El 2026-09-02 y el 2026-09-03 la capa trimestral depositó dos paquetes etiquetados como el trimestre `2026-T3`, cuando el trimestre estaba recién empezado: eran **instantáneas a media vigencia**, no el depósito del trimestre, y contienen el ancla de un mes abierto que después se reescribió. Su contenido no es falso —era una foto verdadera de esos días—; lo que estaba mal era la etiqueta. Se dejan como están. **El depósito del trimestre cerrado está pendiente**: se hará una vez, después del 30 de septiembre, y su propia fecha dirá que se hizo después. Ninguna comprobación lo encontró —los recibos decían «depositado, T3, correcto»—; se encontró preguntando qué había dentro del paquete.

**Discontinuidad de la capa institucional, declarada con esta versión.** Hasta el 2026-09-20 los depósitos de esa capa se hicieron contra `sandbox.zenodo.org`, el banco de pruebas: sus identificadores empiezan por `10.5072` y **no son permanentes** —el servicio los borra cuando quiere, y quien cite uno puede encontrarse con nada—. Los dos que existen son del 2026-09-02 y del 2026-09-03, constan en `testigo/recibos-A.jsonl` con su base, y son los mismos que el párrafo anterior retracta por su etiqueta. **Desde el 2026-09-21 los depósitos se hacen contra `zenodo.org`**, el registro permanente, y el primero de verdad será el del trimestre cerrado, después del 30 de septiembre. Se declara aquí, y no en la tabla del apartado 8, porque aquella tabla habla de cómo se lee una fuente —la usa la regla del nacimiento— y esto no cambia ninguna medida: cambia dónde queda depositada la prueba. Quien compare los recibos anteriores al 21-09 con los siguientes verá dos servicios distintos, y ésta es la razón.

**Discontinuidad de método de la capa que fecha el día, declarada con esta versión.** Hasta el 2026-09-25 el día lo fechaba el **alojamiento de repositorios** donde se publica el testigo: se le empujaba el resumen y se guardaba la hora que decía haberlo recibido. Eso tenía dos defectos que no se arreglan escribiendo con más cuidado —compartía proveedor con el repositorio y con el vigía, y **sólo lo podíamos comprobar nosotros**, así que quien leyera el archivo tenía que creerse nuestro recibo—. **Desde el 2026-09-26 el día lo fechan dos autoridades de sellado RFC 3161 independientes**, en dos países y con dos raíces que no comparten camino de fallo; cada sello viaja entero dentro de su recibo y **cualquiera lo comprueba sin hablar con nosotros ni con la autoridad**. Cada día consta **cuántas de las dos sellaron**. El alojamiento **se queda** con el papel que de verdad sostiene: probar **qué** se publicó y **en qué orden**, nunca cuándo. **Los días anteriores al 2026-09-26 no se tocan**: su capa C es la que tuvieron, se juzga con la regla de entonces, y quien lea el archivo verá dos tramos distintos porque eso es lo que pasó; lo que existe para ellos es el sello de anterioridad del 2026-09-16 sobre la raíz de su cadena, que prueba que existían no más tarde de ese día. **Y la obligación que esto trae, con fecha y no como aspiración:** un sello sólo se puede validar mientras la cadena de su autoridad siga viva —2040 la de una, 2037 la de la otra—, así que **antes de que venza la primera hay que volver a sellar lo ya sellado** con una autoridad vigente, encadenando el nuevo sobre el viejo. Un sello caducado no cuenta como capa, y el verificador avisa antes de que ocurra. El detalle del mecanismo, en la especificación de sellado, que viaja dentro de cada depósito.

**La discontinuidad de Smithery del 2026-09-08 no se declaró entonces**, y se declara ahora en la tabla del apartado 8. Ese día Smithery pasó a leerse con una semilla que fija el orden; volver a medir el día anterior con esa lectura daba otro resultado —de 271 objetos a 11.814—, así que por el criterio del mismo apartado era una discontinuidad. No cambió ningún nacimiento: el día anterior Smithery se había leído cortada, así que ninguna de sus altas del 09-08 podía serlo.

**Corrección de un error del texto, declarada y no disimulada.** Al sacar de la tabla del apartado 1 la fila del historial que llevaba pegada (versión 6), esa fila —la de la versión 4— **no se devolvió a su sitio**, y el historial de la versión 6 perdió la entrada de la versión 4; ya en la 5 la tabla iba fuera de orden. Se restituye con su texto original y la tabla se ordena. Los días sellados con la versión 6 conservan el texto con el error, porque no se resella nada.

**La versión 6 declara una discontinuidad sobre una fuente, y sólo sobre ella.** PulseMCP se leía recorriendo unas 535 páginas de su web; pasa a leerse por el **conjunto** que el propio sitio declara en su sitemap, en una petición. El criterio del apartado 8 se cumple sin duda: volver a medir el mismo día por las dos vías da resultados distintos —el 2026-09-07, 21.957 por el conjunto frente a 21.912 por el recorrido—, y esa diferencia **no es ruido: es lo que la paginación se dejaba**.

**Se puede solapar, y se solapa.** Al contrario que en la versión 5, aquí sí hay dos procedimientos vivos: el recorrido sigue existiendo y se ejecuta como **control periódico**, de modo que la diferencia entre las dos vías quede medida en vez de supuesta. Ese control **registra y no decide**: hasta que haya semanas de esa medida, ningún número sacado de ahí manda sobre nada.

**Lo que la discontinuidad produce el primer día, dicho antes de que salga:** **18 ausencias de golpe**, que son los objetos que el sitio ya no lista y que la paginación seguía trayendo. De ellos, **14 tienen dos testigos independientes** —dejaron de salir por la paginación *y* el sitio los retiró de su conjunto—. Son correctas, y son las primeras bajas de esa fuente con respaldo.

**Y una consecuencia que no es de medida sino de método:** de 535 peticiones a 1. Eso es el apartado 2 —la carga que se le pone al observado— mejorando dos órdenes de magnitud, y es la razón por la que este cambio se hace aunque no arreglara nada más.

**El instrumento deja de parar por recuentos ajenos.** Hasta la versión 5, la enumeración de paquetes paraba cuando el total que declaraba la propia fuente decía que ya estaba. Un recuento de un tercero no se puede comprobar, y si venía corto la lectura quedaba a medias **sin declarar corte**. Ahora se para por un hecho que la fuente entrega —dejar de dar filas— y el recuento declarado se guarda **para contrastarlo**: si no cuadra con lo traído, eso es un corte con los dos números dentro. Es la tercera vez que aparece la misma clase de defecto —Smithery en la versión 2, PulseMCP en la 6— y las cinco fuentes quedan tratando esa dependencia igual.

**Corrección de un error del texto, declarada y no disimulada.** Desde la versión 4, la tabla del apartado 1 traía **una fila del historial de versiones pegada dentro**, entre Smithery y Glama. No cambió ninguna medida —el verificador lee las cinco fuentes por su identificador entre acentos graves, y las cinco salían bien— pero el documento que define el universo observado llevaba seis días sellado con un párrafo que no era suyo. Se corrige aquí. **Los días ya sellados conservan el texto con el error, porque no se resella nada**: quien compare las versiones verá la diferencia, que es justo lo que el apartado 8 pide.

**La versión 5 SÍ es una discontinuidad declarada**, y es la primera. El criterio del apartado 8 lo dice sin ambigüedad: *si volviendo a medir lo de ayer el resultado pudiera salir distinto, es una discontinuidad*. Aquí sale distinto — no porque se mida peor, sino porque **antes esto no se medía**: hasta el 2026-09-06 un objeto que desaparecía de una lista recorrida entera no dejaba rastro en ninguna parte, y desde el 2026-09-07 deja un episodio con su fecha. Volver a medir el 3 de septiembre con este método daría ausencias donde el archivo no tiene ninguna.

**Y no se puede solapar, porque no hay dos procedimientos que solapar: hay uno y ninguno.** El apartado 8 admite saltarse el solape con excusa escrita, y ésta es la excusa: el procedimiento anterior no producía ninguna medida de ausencia con la que calibrar. La consecuencia se declara en vez de disimularse — **los cinco primeros días del archivo (2026-09-02 a 2026-09-06) no tienen serie de ausencias y no la tendrán nunca**, porque sellar hacia atrás está prohibido. Toda cohorte de mortalidad empieza el 2026-09-07, y la población anterior entra en ella cortada por la izquierda, igual que la del primer día en la de nacimiento.

**`N` queda explícitamente sin fijar en esta versión, y ninguna muerte se declara por ausencia.** El día que se fije será otra subida de versión, con su medida delante.

**Sube también el formato del archivo: `strata-sello/4` → `strata-sello/5`.** No añade ningún tipo nuevo de primer nivel —una ausencia tiene objeto, así que entra como una forma más dentro de `observacion`, al revés que la cobertura de fuente, que no tenía ninguno—. Sube porque sin el número un día sin entradas de ausencia sería ambiguo entre *«no faltó nadie»* y *«el instrumento todavía no grababa ausencias»*, que es exactamente la ambigüedad que un número de formato existe para quitar.

**La versión 4 tampoco es una discontinuidad**, y por el mismo criterio del apartado 8: volver a medir lo de ayer no daría un resultado distinto, porque **no se mide nada nuevo**. El estado de cada fuente ya se calculaba y ya decidía quién constaba como nacido; lo único que cambia es que ahora se sella, de modo que pueda comprobarse desde fuera. Se declara igualmente porque cambia el formato del archivo —`strata-sello/3` → `strata-sello/4`— y un cambio de formato se anuncia aunque no mueva ninguna medida.

**Esta subida de versión no es una discontinuidad**, y se puede afirmar con el criterio del apartado 8: volver a medir lo de ayer no daría un resultado distinto, **porque no hay ningún ayer** — no había ni una observación real sellada cuando se hizo el cambio. Es la única ventana en la que ampliar el universo sale gratis.

Después del primer día del archivo, añadir una fuente **sí** sería una discontinuidad declarada: cambiaría lo que la población significa, y además todos los objetos de la fuente nueva entrarían como «ya existía cuando llegamos», empobreciendo para siempre la cohorte de nacidos bajo observación.
