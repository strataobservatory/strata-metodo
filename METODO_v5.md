# Método de observación · Strata Observatory · versión 5

**Qué es este documento.** La descripción completa de cómo observamos, escrita para quien **no se fía de nosotros**. Se sella junto a cada observación que produce, de modo que dentro de diez años se pueda saber no sólo qué medimos sino **cómo lo medimos entonces**.

**Qué no es.** No argumenta que lo que medimos importe. No recomienda nada ni puntúa a nadie. Y no describe cómo se fecha el archivo: eso está en el procedimiento de verificación, que se publica aparte y funciona sin acceso a nuestros datos.

**Alcance de esta versión.** Cubre la **Capa 0 (censo)** y la **Capa 1 (afirmaciones)**. Las sondas de comportamiento —Capa 2— **no están implementadas y no se describen aquí**: prometer un método que no se ejecuta sería exactamente lo que este proyecto no hace.

---

## 1. El universo observado

Tres clases de objeto, que son el mismo ecosistema visto a tres niveles:

1. **Registros y directorios.** Los sitios que listan a los demás.
2. **Servicios listados en ellos.** El grueso de la población.
3. **Servicios y agentes con ficha propia en su dominio**, hallados sondeando rutas estándar sobre dominios ya conocidos.

**Ámbito: global.** No hay eje geográfico —estos objetos no tienen nacionalidad— ni filtro de idioma. Las afirmaciones se archivan en un solo idioma, conservando la referencia y una cita mínima del original en su lengua.

### La regla de inclusión

Un objeto entra en el censo si aparece en alguna de estas fuentes:

- **Listas enumerables** — las cinco nombradas más abajo, y sólo ésas.
- **Rastro de dependencia**, hasta **dos niveles** desde un objeto ya censado. Al segundo nivel sólo entra lo que pertenece a las clases de arriba, no toda dependencia transitiva.
- **Frontera**: sondeo de rutas estándar sobre dominios conocidos, y vigilancia **filtrada por patrón de nombre** de los registros públicos de certificados.

**Ese filtro es parte de la frontera del universo**, no un detalle de implementación: lo que queda fuera del patrón consta como fuera de la regla de inclusión, **no como inexistente**.

### Las cinco listas enumerables, nombradas

La versión 1 decía «registros y directorios públicos» sin nombrar ninguno, y esa vaguedad tuvo una consecuencia medible: se implementaron dos fuentes, y las otras tres **no quedaron excluidas: quedaron ausentes** — sin aparecer siquiera entre los descartes, de modo que nadie podía notar que faltaban. Un universo que no se nombra no se puede auditar.

Se recorren en este orden:

| Orden | Fuente | Identificador en el código |
|---|---|---|
| 1 | Registro oficial del protocolo | `registro-oficial-mcp` |
| 2 | Directorio Smithery | `directorio-smithery` |
| 4 | **apartado 3**: el estado de cada fuente cada día pasa a ser parte del archivo sellado, y el verificador exige que cada día traiga la fila de todas las fuentes que el método de ese día nombra | ese dato es del que depende la regla de nacimiento del apartado 7, y vivía sólo en una base local: no se sellaba, ningún verificador lo miraba y no viajaba en la copia. El producto entero descansaba sobre el único trozo del censo que nadie podía comprobar |
| 3 | Directorio Glama | `directorio-glama` |
| 4 | Directorio PulseMCP | `directorio-pulsemcp` |
| 5 | Repositorios de paquetes, para lo que se declare servicio sin estar listado | `repositorio-npm` |

**La columna del identificador no es decorativa.** Es lo que permite comprobar a máquina que el método y el instrumento dicen lo mismo: si esta tabla nombra una fuente que el censo no intenta, o el censo intenta una que esta tabla no nombra, la verificación falla. El defecto que motivó esta versión queda así convertido en barrera.

Añadir o quitar una fuente de esta tabla es **cambiar el universo observado**, y por tanto una modificación del método con su entrada en el historial — nunca un cambio de configuración.

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

**El agente se identifica siempre**, con un enlace a este documento. Un registro construido escondiéndose no atestigua nada.

**Sólo superficie pública, en sentido estricto**: accesible sin credenciales ajenas, sin rodear ningún control y sin aceptar condiciones que lo prohíban.

**Las señales de exclusión del sitio se respetan como norma absoluta.** Lo que no se pueda observar así consta como **no observable por política** y permanece en el censo con su motivo.

**Carga cero sobre el observado.** Se pregunta si algo ha cambiado antes de descargarlo: se guarda el hash en cada pasada y el contenido **sólo cuando el hash cambia**.

**Si un objeto bloquea el acceso, se registra el bloqueo y se para. No se rodea.** El bloqueo es un dato en sí mismo.

**Si alguien pide dejar de ser observado, se deja de observar** y se registra la petición con su fecha. La serie se cierra con motivo documentado, nunca con un hueco.

**Nunca se observa**: nada tras credenciales de otro, nada referido a personas, y nada que provenga de clientes de quien mantiene el observatorio.

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

La continuidad se establece por **escalera de evidencia**:

1. **Declarada** — el objeto nuevo declara el anterior, o la dirección antigua redirige a la nueva.
2. **Estructural** — mismo repositorio, misma identidad de paquete, mismo mantenedor, misma clave.
3. **Circunstancial** — desaparece uno y aparece otro parecido, con propósito declarado similar, en una ventana corta.

**Los niveles 1 y 2 son el mismo objeto.** Se registra el alias con su fecha y el tipo de evidencia.
**El nivel 3 no lo es**: se graba una muerte y un nacimiento, con una **nota de vínculo sospechado** que deja constancia de la relación posible y de la evidencia que la sugiere.

> **Separar es recuperable; fusionar no.** Unir con evidencia débil deja de contar muertes y hace que la supervivencia salga optimista. Separar de más sobrestima algo la mortalidad, y la nota de vínculo permite reunirlas después. **Se asume ese sesgo pesimista a conciencia, y se dice.**

Casos particulares: en una **bifurcación** el original conserva su identidad y la bifurcación es un objeto nuevo con vínculo declarado de derivación · un **nombre liberado por una muerte** es siempre un objeto nuevo · un objeto **listado en cuatro directorios** es una identidad con cuatro avistamientos, porque las listas son fuentes y no identidades.

Cada decisión de identidad se graba con su evidencia. Revisarla es añadir una entrada, nunca reescribir.

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

### Hacia dónde falla esta regla

**Hacia «no ha muerto».** Un nacimiento no declarado empobrece una cohorte nuestra; una muerte falsa es **una afirmación falsa sobre un tercero**: decir que algo dejó de existir cuando existe. Es la misma familia que «no se intentó» frente a «no nos dejaron», y en esa familia este método elige siempre el mismo lado.

Consecuencia declarada, como la sobrecuenta del apartado 7: **la mortalidad que se publique será una cota inferior.** Se dice, no se disimula.

### Qué se sella, y qué estado de cobertura le toca

**Cada día confirmado de ausencia va dentro del sello**, atado al día en que empezó su episodio, y también la reaparición que lo cierra. Va dentro por lo mismo que el estado de cada fuente entró en la versión 4: es la evidencia de la que dependerá toda afirmación de mortalidad, y quien no pueda recontarla no puede comprobar la afirmación. Se sellan **todos** los días confirmados y no sólo el primero, porque lo que hay que poder recontar es cuántos días se confirmó, no cuántos pasaron.

**Un objeto ausente sigue constando `observado`**, con su motivo escrito. No hay un sexto estado de cobertura: los cinco del apartado 3 contestan *«¿conseguimos mirarlo?»*, y aquí se miró —se recorrió la lista entera—. *«¿Estaba?»* es otra pregunta, con otra forma —un intervalo, no el estado de un día—, y por eso se registra aparte. Meterlas en la misma columna sería repetir el error que el apartado 1 ya prohíbe expresamente: confundir «no nos dejaron mirar» con «miramos y no estaba».

---

## 6. Las afirmaciones

**Qué convierte una declaración en afirmación vigilada:**

> Una afirmación vigilable es una declaración que el objeto hace **sobre sí mismo**, legible por máquina, **cuyo incumplimiento no produce ningún error visible**.

Ésa es la frontera con el censo. «Responde o no responde» es censo: quien llama lo ve. «Declara exponer esta herramienta» es afirmación: si desaparece no salta nada hasta que alguien la llama, y para entonces ya nadie sabe cuándo dejó de estar.

Las afirmaciones **se derivan de la observación del censo y sólo se escriben cuando caen.**

### Las seis familias

| Familia | Enunciado | Cae cuando |
|---|---|---|
| **Capacidades declaradas** | «Declara exponer esta capacidad, con este nombre exacto» — una por capacidad | Desaparece, o **cambia de nombre conservando lo demás**, que es peor porque parece que sigue |
| **Versión declarada** | «Declara esta versión» · y, aparte, «su versión es coherente con su contenido» | La versión retrocede · o **el contenido cambia y la versión no**: un cambio no anunciado |
| **Licencia declarada** | «Declara esta licencia» | Cambia o desaparece |
| **Acceso y autenticación** | «Declara atenderse aquí, con este esquema de autenticación» | Cambia cualquiera de los dos |
| **Procedencia declarada** | «Declara tener su origen aquí» | El origen deja de existir o de ser accesible |
| **Discrepancia declarado/listado** | «Lo que dice de sí mismo y lo que dice de él quien lo lista coinciden en este campo» | Divergen |

Para las fichas propias en dominio hay una séptima: **«declara conformidad con este estándar»**, comprobable contra su esquema.

**En la discrepancia no se dice quién miente.** Se registra el desacuerdo con sus dos fuentes y sus dos fechas. Se describe comportamiento, nunca carácter.

### Qué se guarda cuando una afirmación cae

El enunciado · la fecha en que se sostenía por última vez · la fecha en que se detectó la caída · **la fecha del cambio declarada por el objeto**, si la declara · el fragmento mínimo de evidencia · y la versión de método. Nunca un volcado del contenido ajeno.

La distancia entre las dos fechas —la declarada y la nuestra— es nuestra **resolución real**, y se publica como tal.

### Qué nunca es una afirmación

Lo que falla visiblemente · las descripciones en prosa, que no son falsables · cualquier juicio de calidad · las políticas declaradas de admisión de los directorios · y cualquier cosa referida a personas.

---

## 7. Qué no está medido

Dicho entero, porque es lo que hace citable el resto.

- **El comportamiento real no se mide en esta versión.** Todo lo anterior compara lo declarado contra lo declarado antes. Que un servicio haga lo que dice **no se comprueba**: eso es la Capa 2 y no existe.
- **El censo no es completo.** Sólo alcanza lo que las fuentes del apartado 1 exponen, dentro del filtro declarado.
- **Un objeto puede cambiar y volver** entre dos observaciones diarias sin que lo veamos. La resolución es la cadencia.
- **De la población del primer día no se sabe cuándo nació, y no se sabrá nunca.** Que un objeto naciera bajo observación se afirma comparando la lista de hoy con la de ayer, no creyendo la fecha que el objeto declare —esa no se puede validar—. El primer día no hay ayer contra el que comparar, así que **todo lo censado ese día consta como ya existente** y queda fuera de cualquier cohorte de nacimiento para siempre. Sólo lo que aparece a partir del segundo día tiene una vida entera medible. La fracción de la población que está en cada caso se publica con la serie.
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

**Nunca hacia atrás**: ni se reejecuta un método nuevo sobre datos viejos haciéndolos pasar por originales, ni se reetiquetan observaciones ya selladas. Un error se corrige **añadiendo** una entrada de corrección con su fecha, y el original queda intacto.

---

*Este método es público. El archivo que produce, no. La razón es que el método es replicable y el histórico no lo es: publicarlo no regala nada, y a cambio permite que alguien desconfíe de nosotros y aun así pueda aceptar el dato.*

---

## 9. Historial de versiones de este método

| Versión | Qué cambió | Por qué |
|---|---|---|
| 5 | **apartado 10 nuevo**: la regla de ausencia y muerte, con sus tres puertas, la separación entre ausencia y muerte, la retrofecha de la baja al primer día de ausencia y `N` explícitamente sin fijar. **Apartado 3**: un objeto que falta de una lista recorrida entera consta `observado` con motivo, y no en un sexto estado | el método hablaba de mortalidad y supervivencia en cinco apartados y el instrumento **no tenía la regla**: 49.720 objetos, 0 con día de baja, y la única baja posible era la de una identidad partida en dos. El nacimiento se hizo y su espejo se quedó sin hacer, y la supervivencia necesita los dos. Se escribe **antes de que haya ninguna muerte que contar**, para que la regla no la escriban los datos |
| 1 | — | primera versión |
| 3 | **apartado 7**: se dice que la población del primer día está cortada por la izquierda y no puede entrar en ninguna cohorte de nacimiento, y que el nacimiento se afirma con nuestra cobertura y no con la fecha que el objeto declare | la versión anterior no decía nada de esto, y el instrumento estaba clasificando como «nacido bajo observación» a quien lo **declaraba**: 474 objetos del primer barrido, ninguno visto aparecer. Dejar que una declaración —que no se puede validar— decida una clasificación nuestra es lo que el apartado 4 prohíbe |
| 2 | **apartado 1**: las cinco listas enumerables pasan a estar **nombradas**, con su orden de recorrido, y se añade la regla de que cada una consta como *enumerada*, *excluida* o *ilegible*, nunca omitida en silencio | la versión 1 decía «registros y directorios públicos» sin nombrarlos. El instrumento implementó dos de cinco y las otras tres quedaron **ausentes**, no excluidas: no aparecían ni en los resultados ni en los descartes. Un universo que no se nombra no se puede auditar |

**La versión 5 SÍ es una discontinuidad declarada**, y es la primera. El criterio del apartado 8 lo dice sin ambigüedad: *si volviendo a medir lo de ayer el resultado pudiera salir distinto, es una discontinuidad*. Aquí sale distinto — no porque se mida peor, sino porque **antes esto no se medía**: hasta el 2026-09-06 un objeto que desaparecía de una lista recorrida entera no dejaba rastro en ninguna parte, y desde el 2026-09-07 deja un episodio con su fecha. Volver a medir el 3 de septiembre con este método daría ausencias donde el archivo no tiene ninguna.

**Y no se puede solapar, porque no hay dos procedimientos que solapar: hay uno y ninguno.** El apartado 8 admite saltarse el solape con excusa escrita, y ésta es la excusa: el procedimiento anterior no producía ninguna medida de ausencia con la que calibrar. La consecuencia se declara en vez de disimularse — **los cinco primeros días del archivo (2026-09-02 a 2026-09-06) no tienen serie de ausencias y no la tendrán nunca**, porque sellar hacia atrás está prohibido. Toda cohorte de mortalidad empieza el 2026-09-07, y la población anterior entra en ella cortada por la izquierda, igual que la del primer día en la de nacimiento.

**`N` queda explícitamente sin fijar en esta versión, y ninguna muerte se declara por ausencia.** El día que se fije será otra subida de versión, con su medida delante.

**Sube también el formato del archivo: `strata-sello/4` → `strata-sello/5`.** No añade ningún tipo nuevo de primer nivel —una ausencia tiene objeto, así que entra como una forma más dentro de `observacion`, al revés que la cobertura de fuente, que no tenía ninguno—. Sube porque sin el número un día sin entradas de ausencia sería ambiguo entre *«no faltó nadie»* y *«el instrumento todavía no grababa ausencias»*, que es exactamente la ambigüedad que un número de formato existe para quitar.

**La versión 4 tampoco es una discontinuidad**, y por el mismo criterio del apartado 8: volver a medir lo de ayer no daría un resultado distinto, porque **no se mide nada nuevo**. El estado de cada fuente ya se calculaba y ya decidía quién constaba como nacido; lo único que cambia es que ahora se sella, de modo que pueda comprobarse desde fuera. Se declara igualmente porque cambia el formato del archivo —`strata-sello/3` → `strata-sello/4`— y un cambio de formato se anuncia aunque no mueva ninguna medida.

**Esta subida de versión no es una discontinuidad**, y se puede afirmar con el criterio del apartado 8: volver a medir lo de ayer no daría un resultado distinto, **porque no hay ningún ayer** — no había ni una observación real sellada cuando se hizo el cambio. Es la única ventana en la que ampliar el universo sale gratis.

Después del primer día del archivo, añadir una fuente **sí** sería una discontinuidad declarada: cambiaría lo que la población significa, y además todos los objetos de la fuente nueva entrarían como «ya existía cuando llegamos», empobreciendo para siempre la cohorte de nacidos bajo observación.
