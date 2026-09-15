# Método de observación · Strata Observatory · versión 1

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

- **Listas enumerables** — registros y directorios públicos, y repositorios de paquetes para lo que se declare servicio sin estar listado.
- **Rastro de dependencia**, hasta **dos niveles** desde un objeto ya censado. Al segundo nivel sólo entra lo que pertenece a las clases de arriba, no toda dependencia transitiva.
- **Frontera**: sondeo de rutas estándar sobre dominios conocidos, y vigilancia **filtrada por patrón de nombre** de los registros públicos de certificados.

**Ese filtro es parte de la frontera del universo**, no un detalle de implementación: lo que queda fuera del patrón consta como fuera de la regla de inclusión, **no como inexistente**.

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
