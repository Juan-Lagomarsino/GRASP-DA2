---
theme: default
title: GRASP — Patrones para la Asignación de Responsabilidades
info: |
  Presentación compacta de los 9 patrones GRASP.
  Diseño de Aplicaciones 1 — Cátedra de Ingeniería de Software.
  Versión de clase: ~15–20 min, 6 integrantes.
class: text-center
transition: slide-left
mdc: true
fonts:
  sans: Inter
  mono: Fira Code
---

# G.R.A.S.P.

### Patrones Generales de Software para la Asignación de Responsabilidades

<div class="pt-6 opacity-80 text-sm">
Diseño de Aplicaciones 1 · Cátedra de Ingeniería de Software
</div>

<div class="pt-10 text-sm leading-7 opacity-90">
Integrante 1 · Integrante 2 · Integrante 3<br>
Integrante 4 · Integrante 5 · Integrante 6
</div>

<!--
GUION — Presenta: INTEGRANTE 1 (portada, ~20 s)

Buenos días. Somos [equipo] y hoy les vamos a presentar los patrones GRASP:
los principios generales para asignar responsabilidades a los objetos en el
diseño orientado a objetos. Lo vamos a dividir entre los seis, cada uno toma
uno o dos patrones. Arranco yo con la introducción y el primer patrón.
-->

---
layout: two-cols
class: text-sm
---

# ¿Qué es GRASP?

Principios fundamentales para **asignar responsabilidades** a objetos, expresados como **patrones**.

**¿Qué es una responsabilidad?**
Un contrato u obligación de una clase. Por ejemplo:

- **Hacer** algo (un cálculo, crear un objeto)
- **Iniciar** una acción sobre otro objeto
- **Controlar / coordinar** actividades de otros

::right::

<div class="pl-6 pt-14">

**En diseño**, las responsabilidades se traducen en:

- métodos de una clase, o
- colaboraciones entre varias clases

Un **patrón** = nombre + problema/contexto + solución.

</div>

<!--
GUION — INTEGRANTE 1 (~40 s)

GRASP son las siglas de "Patrones Generales para la Asignación de
Responsabilidades". La pregunta central del diseño orientado a objetos es:
¿quién hace qué? Es decir, a qué clase le doy cada responsabilidad.

Una responsabilidad, según UML, es un contrato u obligación de una clase.
Puede ser HACER algo (un cálculo, crear un objeto), INICIAR una acción sobre
otro objeto, o CONTROLAR el trabajo de otros. En el código, esas
responsabilidades terminan siendo métodos de una clase o colaboraciones entre
varias.

Y cada GRASP es un patrón: tiene un nombre, un problema típico y una solución
recomendada. Vamos a ver los nueve.
-->

---
class: text-sm
---

# Los 9 patrones GRASP

<div class="grid grid-cols-3 gap-4 pt-4">

<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>1 · Creador</b><br><span class="opacity-70">¿quién crea?</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>2 · Experto</b><br><span class="opacity-70">¿quién sabe?</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>3 · Bajo Acoplamiento</b><br><span class="opacity-70">menos dependencias</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>4 · Alta Cohesión</b><br><span class="opacity-70">responsabilidades afines</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>5 · Controlador</b><br><span class="opacity-70">¿quién atiende eventos?</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>6 · Polimorfismo</b><br><span class="opacity-70">variar por tipo</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>7 · Fabricación Pura</b><br><span class="opacity-70">clase artificial</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>8 · Indirección</b><br><span class="opacity-70">intermediario</span>
</div>
<div class="p-3 rounded bg-blue-50 dark:bg-blue-900/30">
<b>9 · Variaciones Protegidas</b><br><span class="opacity-70">interfaz estable</span>
</div>

</div>

<div class="pt-6 text-center opacity-70">Objetivo transversal: <b>bajo acoplamiento</b> y <b>alta cohesión</b>.</div>

<!--
GUION — INTEGRANTE 1 (~25 s)

Estos son los nueve. Los primeros cinco son los más usados en el día a día:
Creador, Experto, Bajo Acoplamiento, Alta Cohesión y Controlador. Los otros
cuatro —Polimorfismo, Fabricación Pura, Indirección y Variaciones
Protegidas— aparecen cuando el diseño se complica. La idea que atraviesa todo
es la misma: mantener bajo el acoplamiento y alta la cohesión. Empecemos por
el Creador.
-->

---

# 1 · Creador

<div class="grid grid-cols-2 gap-8 pt-2 text-sm">
<div>

**Problema:** ¿quién debería crear una nueva instancia de una clase A?

**Solución:** asignarle la creación a la clase **B** si B…

- **agrega / contiene / registra** objetos A
- tiene los **datos de inicialización** de A
- usa A de cerca (es experta en crearlo)

<div class="pt-3 opacity-80">
Ej.: la <b>Factura</b> contiene sus <b>LíneaFactura</b> → la Factura las crea.
</div>

</div>
<div class="flex items-center justify-center">
  <img src="/creador.png" class="max-h-72 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 1 (~40 s)

El patrón Creador responde a una pregunta muy concreta: cuando necesito un
objeto nuevo, ¿quién lo crea? La respuesta es: que lo cree la clase que ya
tiene una relación fuerte con él. En criollo: la clase que lo contiene, que lo
agrega, que lo registra, o que tiene los datos para inicializarlo.

El ejemplo clásico es Factura y LíneaFactura. Como una Factura contiene muchas
líneas —lo ven en el diagrama, con el rombo de composición y la multiplicidad
uno a muchos— entonces la Factura es la candidata natural para crear las
líneas. Evitamos así repartir la creación por cualquier lado.

Con esto cierro mi parte y le paso a [Integrante 2] con el Experto.
-->

---
layout: section
---

# 2 · Experto en Información
<div class="text-base opacity-70 pt-2">Presenta: Integrante 2</div>

<!--
GUION — INTEGRANTE 2 (transición, ~10 s)

Gracias. Yo tomo el patrón más importante de todos, el que está detrás de casi
todas las decisiones: el Experto en Información.
-->

---

# 2 · Experto en Información

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cuál es el principio básico para asignar responsabilidades en POO?

**Solución:** asignar la responsabilidad a la **clase que tiene la información** necesaria para cumplirla — el *experto en información*.

<div class="pt-3">

¿Quién conoce el **total** de la Factura?
→ La **Factura**: es la única que conoce todas sus líneas y sus subtotales.

</div>
</div>
<div class="flex items-center justify-center">
  <img src="/experto_clases.png" class="max-h-80 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 2 (~50 s)

El Experto es el principio fundamental: le doy la responsabilidad a la clase
que tiene la información para cumplirla. Suena obvio, pero es potentísimo.

Miren el ejemplo. ¿Quién debería saber el TOTAL de una factura? Uno podría
pensar en una clase "controlador" que sepa todo, pero no: la que tiene la
información es la Factura, porque es la única que conoce todas sus líneas.
Entonces el método Total() va en Factura.

Y esto se aplica en cascada: para el total, la Factura necesita el subtotal de
cada línea. ¿Quién sabe el subtotal? La LíneaFactura, porque conoce la cantidad
y el producto. Fíjense cómo aplicando el mismo criterio dos veces ya nos
aparecen las clases y sus métodos. Lo vemos en la secuencia.
-->

---
layout: center
---

# Experto → delegación

<img src="/experto_secuencia.png" class="max-h-96 mx-auto rounded shadow" />

<div class="text-center text-sm opacity-80 pt-3">
Subtotal = <code>LíneaFactura.cantidad() × Producto.precioUnitario()</code> → cada quien aporta lo que sabe.
</div>

<!--
GUION — INTEGRANTE 2 (~45 s)

Este diagrama de secuencia muestra el Experto en acción. El actor le pide el
Total a la Factura. La Factura no calcula todo sola: recorre sus líneas y a
cada una le pide su subtotal. Cada LíneaFactura, para su subtotal, usa su
propia cantidad y le pide el precio unitario al Producto.

O sea: cada clase aporta exactamente lo que sabe, y nadie mete la mano en datos
que no le corresponden. Eso es Experto, y de yapa nos da bajo acoplamiento
porque cada objeto habla solo con quien tiene que hablar.

Le paso a [Integrante 3], que va a ver justamente acoplamiento y cohesión.
-->

---
layout: section
---

# 3 · Bajo Acoplamiento y Alta Cohesión
<div class="text-base opacity-70 pt-2">Presenta: Integrante 3</div>

<!--
GUION — INTEGRANTE 3 (transición, ~10 s)

Estos dos patrones son en realidad las dos métricas que guían a todos los
demás. Los vemos juntos porque van de la mano.
-->

---

# 3 · Bajo Acoplamiento

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cómo reducir el impacto de un cambio?

**Solución:** asignar responsabilidades de modo que el **acoplamiento se mantenga bajo**.

- Una clase con bajo acoplamiento **depende de pocas clases**.
- Es peor aún si depende de una clase **inestable**.
- Acoplamiento 0 no existe: los objetos colaboran (es POO).

</div>
<div class="flex flex-col items-center justify-center">
  <img src="/acoplamiento.png" class="max-h-64 rounded shadow" />
  <div class="text-xs opacity-70 pt-2">Class0 y Class3: demasiadas dependencias.</div>
</div>
</div>

<!--
GUION — INTEGRANTE 3 (~40 s)

Acoplamiento es cuánto depende una clase de otras. El problema que resuelve
este patrón es el impacto del cambio: si toco una clase muy acoplada, rompo
media aplicación.

La solución es repartir responsabilidades para que cada clase dependa de pocas
—y sobre todo que no dependa de clases inestables, que cambian seguido—. En el
diagrama, Class0 y Class3 apuntan a un montón de clases: eso es alto
acoplamiento, y es una señal de alarma. Ojo: acoplamiento cero no existe,
porque en objetos las clases tienen que colaborar. La meta es que sea bajo, no
nulo.
-->

---

# 3 · Alta Cohesión

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cómo mantener la complejidad manejable?

**Solución:** asignar responsabilidades para que la clase quede **cohesiva** — que sus métodos sean *afines* y trabajen juntos.

Una clase con **baja cohesión**:

- es difícil de comprender y de reutilizar
- es delicada: los cambios la afectan seguido

</div>
<div class="flex flex-col items-center justify-center">
  <img src="/cohesion.png" class="max-h-72 rounded shadow" />
  <div class="text-xs opacity-70 pt-2">Empleado mezcla datos de RRHH con credenciales.</div>
</div>
</div>

<!--
GUION — INTEGRANTE 3 (~40 s)

Cohesión es lo contrario: mide qué tan relacionadas están las
responsabilidades DENTRO de una clase. Queremos alta cohesión, o sea que todo
lo que hace la clase apunte a un mismo propósito bien definido.

El ejemplo de la clase Empleado es baja cohesión: mezcla datos de recursos
humanos —nombre, cargo, sueldo— con datos de seguridad como usuario y
contraseña. Son cosas no afines. Una clase así es difícil de entender, difícil
de reutilizar y se rompe con cualquier cambio. Conviene separarla.
-->

---
layout: center
class: text-center
---

# El yin-yang: cohesión y acoplamiento

<div class="text-sm max-w-2xl mx-auto pt-4 leading-7">

No hay una relación matemática exacta, **pero se acompañan**:

<div class="pt-3 text-lg">
Baja cohesión ⇢ normalmente <b>alto acoplamiento</b>
</div>

<div class="pt-3 opacity-80">
Una clase que "hace de todo" termina necesitando datos de muchas otras.
Por eso los GRASP siempre empujan hacia <b>alta cohesión</b> y <b>bajo acoplamiento</b>.
</div>
</div>

<!--
GUION — INTEGRANTE 3 (~30 s)

Y acá está la conexión entre los dos. No es una fórmula, pero en la práctica
van juntos: cuando una clase tiene baja cohesión —hace de todo— casi siempre
termina con alto acoplamiento, porque para hacer tantas cosas distintas
necesita datos de muchas otras clases. Por eso, la regla de oro es: apuntar
siempre a alta cohesión y bajo acoplamiento. Todos los demás GRASP se juzgan
con esta vara. Sigue [Integrante 4] con Controlador y Polimorfismo.
-->

---
layout: section
---

# 4 · Controlador y Polimorfismo
<div class="text-base opacity-70 pt-2">Presenta: Integrante 4</div>

<!--
GUION — INTEGRANTE 4 (transición, ~10 s)

Gracias. Yo tomo dos patrones: primero el Controlador, que decide quién recibe
los eventos, y después Polimorfismo.
-->

---

# 4 · Controlador

<div class="text-sm pt-1">

**Problema:** ¿quién atiende los **eventos del sistema** (acciones del usuario u otros sistemas)?
**Solución:** una clase **controlador** que no sea la interfaz de usuario y que **delegue** el trabajo real.

</div>

<div class="grid grid-cols-2 gap-6 pt-3">
<div class="flex flex-col items-center">
  <div class="text-xs font-bold pb-1">Controlador de Fachada (todo el sistema)</div>
  <img src="/controlador_fachada.png" class="max-h-56 rounded shadow" />
</div>
<div class="flex flex-col items-center">
  <div class="text-xs font-bold pb-1">Controlador de Caso de Uso (uno por caso)</div>
  <img src="/controlador_casos.png" class="max-h-56 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 4 (~50 s)

El Controlador responde: cuando llega un evento del sistema —el usuario aprieta
un botón, u otro sistema nos manda un pedido— ¿qué clase lo recibe? La regla es
que NO lo reciba la interfaz gráfica directamente, sino una clase controlador,
que después delega el trabajo a las clases del dominio.

Hay dos sabores. A la izquierda, el Controlador de Fachada: una sola clase para
todo el sistema, sirve cuando hay pocos eventos. A la derecha, el Controlador
de Caso de Uso: uno por cada caso de uso —ClientesCtrl, VentasCtrl,
ComprasCtrl—, que conviene cuando la fachada empezaría a hacer demasiado y
perdería cohesión. Lo importante: el controlador coordina, no hace todo él
mismo.
-->

---

# 4 · Polimorfismo

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cómo manejar alternativas **según el tipo** de un objeto, sin llenar el código de `if`?

**Solución:** distribuir el comportamiento con **operaciones polimórficas**, una por cada tipo.

<div class="pt-2 opacity-80">
Cada instrumento sabe <b>afinarse</b> a su manera → <code>Afinar()</code> en cada clase.
</div>

<div class="pt-3">
✅ Diseño <b>abierto a la extensión, cerrado al cambio</b> (Principio Abierto/Cerrado).
</div>
</div>
<div class="flex items-center justify-center">
  <img src="/polimorfismo.png" class="max-h-80 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 4 (~45 s)

Polimorfismo ataca un olor de código muy común: los "if" o "switch" que
preguntan de qué tipo es un objeto para decidir qué hacer. Cada vez que agregás
un tipo nuevo, tenés que tocar ese if. Mal.

La solución es el polimorfismo: definir una operación común —acá Afinar()— en
una interfaz o clase base, y que cada tipo la implemente a su manera. El
afinador solo dice "afinate", y cada instrumento —piano, guitarra, bajo— sabe
cómo hacerlo. Para agregar un instrumento nuevo, creo una clase más y no toco
nada del código existente. Eso es el Principio Abierto/Cerrado: abierto a
extender, cerrado a modificar. Le paso a [Integrante 5].
-->

---
layout: section
---

# 5 · Fabricación Pura e Indirección
<div class="text-base opacity-70 pt-2">Presenta: Integrante 5</div>

<!--
GUION — INTEGRANTE 5 (transición, ~10 s)

Gracias. Yo tomo dos patrones que sirven para desacoplar: Fabricación Pura e
Indirección.
-->

---

# 5 · Fabricación Pura

<div class="text-sm pt-1">

**Problema:** ¿a quién le doy una responsabilidad cuando ponerla en una clase del dominio **baja la cohesión o sube el acoplamiento**?
**Solución:** crear una **clase artificial** (que no representa nada del dominio) con un conjunto cohesivo de responsabilidades.

</div>

<div class="grid grid-cols-2 gap-6 pt-3">
<div class="flex flex-col items-center">
  <div class="text-xs font-bold pb-1">Antes: Factura exporta PDF</div>
  <img src="/fabricacion_antes.png" class="max-h-52 rounded shadow" />
</div>
<div class="flex flex-col items-center">
  <div class="text-xs font-bold pb-1">Después: GeneradorPDF (fabricación pura)</div>
  <img src="/fabricacion_despues.png" class="max-h-52 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 5 (~50 s)

A veces el Experto nos lleva a un mal lugar. Miren "antes": la Factura calcula
el total, el IVA... y también exporta a PDF. Exportar a PDF es un tema técnico,
no es del dominio del negocio. Metido en Factura le baja la cohesión y la acopla
a la librería de PDF.

Fabricación Pura dice: cuando pase esto, inventá una clase artificial que no
representa nada del dominio, solo para agrupar esa responsabilidad de forma
cohesiva. En "después" creamos GeneradorPDF: la Factura vuelve a ocuparse solo
de lo suyo, y la parte técnica queda aislada y reutilizable. Ganamos cohesión y
bajamos acoplamiento.
-->

---

# 5 · Indirección

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cómo **desacoplar** dos elementos para que el acoplamiento sea bajo pero se mantenga el potencial de reuso?

**Solución:** asignar la responsabilidad a un **objeto intermediario** que medie entre ambos.

<div class="pt-2 opacity-80">
El <b>Usuario</b> no conoce al <code>ServicioCorreo</code> concreto: habla con la interfaz <code>INotificador</code>.
</div>

<div class="pt-3 opacity-70">
Un intermediario de indirección suele ser también una <b>Fabricación Pura</b>.
</div>
</div>
<div class="flex items-center justify-center">
  <img src="/indireccion_despues.png" class="max-h-72 rounded shadow" />
</div>
</div>

<!--
GUION — INTEGRANTE 5 (~45 s)

Indirección es primo hermano de lo anterior. El problema: si una clase le habla
directo a otra —o a una API externa— queda pegada a los detalles de esa otra.
Si la API cambia, tengo que tocar mi clase.

La solución es meter un intermediario en el medio. En el ejemplo, el Usuario no
llama directo al ServicioCorreo: llama a una interfaz, INotificador. El
ServicioCorreo implementa esa interfaz. Así el Usuario queda desacoplado del
servicio concreto, y mañana puedo cambiar el correo por un SMS sin tocar al
Usuario. De hecho, ese intermediario muchas veces es también una Fabricación
Pura. Cierra [Integrante 6] con Variaciones Protegidas.
-->

---
layout: section
---

# 6 · Variaciones Protegidas
<div class="text-base opacity-70 pt-2">Presenta: Integrante 6</div>

<!--
GUION — INTEGRANTE 6 (transición, ~10 s)

Gracias. Yo cierro con el patrón que engloba a varios de los anteriores:
Variaciones Protegidas, más una ley de diseño muy útil.
-->

---

# 6 · Variaciones Protegidas

<div class="grid grid-cols-2 gap-8 text-sm pt-2">
<div>

**Problema:** ¿cómo diseñar para que las **variaciones** de una parte no impacten al resto?

**Solución:** identificar los puntos que pueden variar y **envolverlos con una interfaz estable**.

- no acoplarse a tipos concretos
- favorecer el polimorfismo
- desacoplar con indirección

</div>
<div class="flex flex-col items-center justify-center">
  <img src="/variaciones.png" class="max-h-64 rounded shadow" />
  <div class="text-xs opacity-70 pt-2">Cambiar de proveedor solo afecta a su adaptador.</div>
</div>
</div>

<!--
GUION — INTEGRANTE 6 (~50 s)

Variaciones Protegidas es como el patrón paraguas: la idea es predecir qué
partes del sistema van a cambiar y protegerlas detrás de una interfaz estable,
para que ese cambio no se propague.

En el ejemplo tenemos proveedores de temperatura distintos: Google y Microsoft,
cada uno con su API rara. En vez de que el programa dependa de cada API, ponemos
un TemperatureAdapter con un método estable, GetTemperature(). Cada proveedor
tiene su adaptador. Si mañana entra un proveedor nuevo, solo agrego un adaptador
y todo lo demás sigue igual. Fíjense que esto usa polimorfismo e indirección
por debajo: es la síntesis de varios GRASP.
-->

---

# Ley de Demeter

<div class="text-sm pt-1">

*"No hables con extraños"*: una clase debe evitar conocer la **estructura interna** de objetos indirectos.

</div>

<div class="grid grid-cols-2 gap-8 pt-3 text-sm">
<div class="flex items-center justify-center">
  <img src="/demeter_bien.png" class="max-h-64 rounded shadow" />
</div>
<div class="flex flex-col justify-center">

❌ El Comercio pide la Billetera del Cliente y opera sobre ella
→ queda acoplado a la estructura interna.

✅ El Comercio le pide al **Cliente** que pague (`GetPagar`)
→ el Cliente maneja su Billetera. **Menos acoplamiento.**

</div>
</div>

<!--
GUION — INTEGRANTE 6 (~40 s)

Cerramos con una ley muy práctica que va de la mano con estos patrones: la Ley
de Demeter, o "no hables con extraños". Dice que un objeto no debería meterse en
las tripas de otro.

El caso: un Comercio quiere cobrarle a un Cliente. La forma incorrecta es que el
Comercio le pida la Billetera al Cliente y opere directamente sobre esa
billetera —ahí el Comercio quedó acoplado a cómo está hecho el Cliente por
dentro—. La forma correcta, que ven en la secuencia, es que el Comercio le pida
al Cliente "pagá este monto", y que el Cliente se encargue de su propia
billetera. El Comercio solo habla con quien conoce directo. Menos acoplamiento,
diseño más robusto.
-->

---
layout: center
class: text-center
---

# En resumen

<div class="max-w-3xl mx-auto text-sm leading-7 pt-2">

Aplicar cualquier GRASP **nunca** debe ir en contra de las métricas del buen diseño:
**alta cohesión** y **bajo acoplamiento**.

<div class="grid grid-cols-3 gap-3 pt-6 text-left text-xs">
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Creador · Experto</div>
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Bajo Acoplamiento · Alta Cohesión</div>
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Controlador</div>
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Polimorfismo</div>
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Fabricación Pura · Indirección</div>
<div class="p-2 rounded bg-gray-100 dark:bg-gray-800">Variaciones Protegidas</div>
</div>

<div class="pt-8 text-lg">¡Gracias! ¿Preguntas?</div>

</div>

<!--
GUION — INTEGRANTE 6 (cierre, ~25 s)

Para cerrar, la idea que se llevan de todo esto: los nueve patrones GRASP son
herramientas para decidir quién hace qué, pero ninguno se aplica a ciegas.
Cohesión es qué tan asociadas están las responsabilidades de una clase;
acoplamiento, qué tan atada está a otras. Todo GRASP se valida contra esas dos
métricas: alta cohesión, bajo acoplamiento. Con eso cerramos. Muchas gracias,
quedamos para las preguntas.
-->
