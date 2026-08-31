# Guion de presentación — GRASP

**Duración total estimada: ~16–19 min** · 6 integrantes · ~3 min cada uno.

Cada integrante presenta 1–2 patrones. El guion completo también está embebido
en las **notas del orador** de cada diapositiva (se ven en el *modo presentador*
de Slidev, tecla **`p`**). Este documento es para repartir, estudiar y ensayar.

> Reemplacen "Integrante N" por los nombres reales en la portada de `slides.md`
> y en los separadores de sección.

| # | Integrante | Temas | Diapositivas | Tiempo |
|---|-----------|-------|--------------|--------|
| 1 | Integrante 1 | Introducción + **Creador** | Portada → Creador (4) | ~2:30 |
| 2 | Integrante 2 | **Experto en Información** | Sección 2 → Secuencia (3) | ~2:30 |
| 3 | Integrante 3 | **Bajo Acoplamiento** + **Alta Cohesión** | Sección 3 → yin-yang (4) | ~3:00 |
| 4 | Integrante 4 | **Controlador** + **Polimorfismo** | Sección 4 → Polimorfismo (3) | ~3:00 |
| 5 | Integrante 5 | **Fabricación Pura** + **Indirección** | Sección 5 → Indirección (3) | ~3:00 |
| 6 | Integrante 6 | **Variaciones Protegidas** + **Ley de Demeter** + cierre | Sección 6 → Gracias (4) | ~2:45 |

---

## Integrante 1 — Introducción + Creador (~2:30)

**Portada (~20 s)**
Buenos días. Somos [equipo] y hoy les vamos a presentar los patrones GRASP: los
principios generales para asignar responsabilidades a los objetos en el diseño
orientado a objetos. Lo dividimos entre los seis, cada uno toma uno o dos
patrones. Arranco yo con la introducción y el primer patrón.

**¿Qué es GRASP? (~40 s)**
GRASP son las siglas de "Patrones Generales para la Asignación de
Responsabilidades". La pregunta central del diseño orientado a objetos es:
¿quién hace qué?, es decir, a qué clase le doy cada responsabilidad. Una
responsabilidad, según UML, es un contrato u obligación de una clase: puede ser
HACER algo, INICIAR una acción sobre otro objeto, o CONTROLAR el trabajo de
otros. En el código terminan siendo métodos de una clase o colaboraciones entre
varias. Cada GRASP es un patrón: nombre, problema y solución.

**Los 9 patrones (~25 s)**
Estos son los nueve. Los primeros cinco son los más usados: Creador, Experto,
Bajo Acoplamiento, Alta Cohesión y Controlador. Los otros cuatro aparecen cuando
el diseño se complica. La idea que atraviesa todo es la misma: mantener bajo el
acoplamiento y alta la cohesión.

**Creador (~40 s)**
El patrón Creador responde: cuando necesito un objeto nuevo, ¿quién lo crea? Que
lo cree la clase que ya tiene una relación fuerte con él: la que lo contiene, lo
agrega, lo registra, o tiene sus datos de inicialización. El ejemplo clásico es
Factura y LíneaFactura: como una Factura contiene muchas líneas —vean el rombo
de composición, uno a muchos— la Factura es la candidata natural para crearlas.
Le paso a [Integrante 2] con el Experto.

---

## Integrante 2 — Experto en Información (~2:30)

**Transición (~10 s)**
Gracias. Yo tomo el patrón más importante, el que está detrás de casi todas las
decisiones: el Experto en Información.

**Experto — problema y solución (~50 s)**
El Experto es el principio fundamental: le doy la responsabilidad a la clase que
tiene la información para cumplirla. ¿Quién debería saber el TOTAL de una
factura? Uno podría pensar en un "controlador" que sepa todo, pero no: la que
tiene la información es la Factura, porque es la única que conoce todas sus
líneas. Entonces Total() va en Factura. Y se aplica en cascada: para el total,
la Factura necesita el subtotal de cada línea; ¿quién sabe el subtotal? La
LíneaFactura, porque conoce la cantidad y el producto. Aplicando el mismo
criterio dos veces ya aparecen las clases y sus métodos.

**Experto — delegación / secuencia (~45 s)**
Este diagrama de secuencia muestra el Experto en acción. El actor le pide el
Total a la Factura. La Factura no calcula todo sola: recorre sus líneas y a cada
una le pide su subtotal. Cada LíneaFactura usa su cantidad y le pide el precio
unitario al Producto. Cada clase aporta lo que sabe y nadie mete la mano donde
no le corresponde. Eso es Experto, y de yapa da bajo acoplamiento. Le paso a
[Integrante 3].

---

## Integrante 3 — Bajo Acoplamiento + Alta Cohesión (~3:00)

**Transición (~10 s)**
Estos dos patrones son en realidad las dos métricas que guían a todos los demás.
Los vemos juntos porque van de la mano.

**Bajo Acoplamiento (~40 s)**
Acoplamiento es cuánto depende una clase de otras. El problema que resuelve es
el impacto del cambio: si toco una clase muy acoplada, rompo media aplicación.
La solución es repartir responsabilidades para que cada clase dependa de pocas,
y que no dependa de clases inestables. En el diagrama, Class0 y Class3 apuntan a
muchas clases: eso es alto acoplamiento, señal de alarma. Ojo: acoplamiento cero
no existe, porque en objetos las clases colaboran. La meta es bajo, no nulo.

**Alta Cohesión (~40 s)**
Cohesión es lo contrario: qué tan relacionadas están las responsabilidades
DENTRO de una clase. Queremos alta cohesión: que todo lo que hace apunte a un
mismo propósito. La clase Empleado del ejemplo tiene baja cohesión: mezcla datos
de RRHH —nombre, cargo, sueldo— con datos de seguridad —usuario, contraseña—.
Son cosas no afines. Una clase así es difícil de entender, de reutilizar, y se
rompe con cualquier cambio.

**El yin-yang (~30 s)**
Acá está la conexión. No es una fórmula, pero van juntos: cuando una clase tiene
baja cohesión —hace de todo— casi siempre termina con alto acoplamiento, porque
necesita datos de muchas otras. La regla de oro: apuntar siempre a alta cohesión
y bajo acoplamiento. Todos los demás GRASP se juzgan con esta vara. Sigue
[Integrante 4].

---

## Integrante 4 — Controlador + Polimorfismo (~3:00)

**Transición (~10 s)**
Gracias. Yo tomo dos patrones: el Controlador, que decide quién recibe los
eventos, y después Polimorfismo.

**Controlador (~50 s)**
El Controlador responde: cuando llega un evento del sistema —el usuario aprieta
un botón, u otro sistema nos manda un pedido— ¿qué clase lo recibe? La regla es
que NO lo reciba la interfaz gráfica, sino una clase controlador, que delega el
trabajo real al dominio. Hay dos sabores: el Controlador de Fachada, una sola
clase para todo el sistema (pocos eventos); y el Controlador de Caso de Uso, uno
por caso de uso —ClientesCtrl, VentasCtrl, ComprasCtrl—, cuando la fachada
perdería cohesión. El controlador coordina, no hace todo él mismo.

**Polimorfismo (~45 s)**
Polimorfismo ataca un olor de código común: los "if" o "switch" que preguntan de
qué tipo es un objeto para decidir qué hacer. Cada tipo nuevo obliga a tocar ese
if. La solución: definir una operación común —Afinar()— en una interfaz o clase
base, y que cada tipo la implemente a su manera. El afinador solo dice
"afinate", y cada instrumento sabe cómo. Para agregar uno nuevo, creo una clase
más y no toco lo existente: Principio Abierto/Cerrado. Le paso a [Integrante 5].

---

## Integrante 5 — Fabricación Pura + Indirección (~3:00)

**Transición (~10 s)**
Gracias. Yo tomo dos patrones para desacoplar: Fabricación Pura e Indirección.

**Fabricación Pura (~50 s)**
A veces el Experto nos lleva a un mal lugar. En "antes", la Factura calcula
total, IVA... y también exporta a PDF. Exportar a PDF es técnico, no es del
dominio: metido en Factura le baja la cohesión y la acopla a la librería de PDF.
Fabricación Pura dice: inventá una clase artificial, que no representa nada del
dominio, solo para agrupar esa responsabilidad de forma cohesiva. En "después"
creamos GeneradorPDF: la Factura vuelve a lo suyo y la parte técnica queda
aislada y reutilizable. Ganamos cohesión y bajamos acoplamiento.

**Indirección (~45 s)**
Indirección es primo hermano. Si una clase le habla directo a otra —o a una API
externa— queda pegada a sus detalles; si esa cambia, tengo que tocar mi clase.
La solución: un intermediario en el medio. El Usuario no llama directo al
ServicioCorreo: llama a la interfaz INotificador, que ServicioCorreo implementa.
Así puedo cambiar correo por SMS sin tocar al Usuario. Ese intermediario muchas
veces es también una Fabricación Pura. Cierra [Integrante 6].

---

## Integrante 6 — Variaciones Protegidas + Ley de Demeter + cierre (~2:45)

**Transición (~10 s)**
Gracias. Yo cierro con el patrón que engloba a varios: Variaciones Protegidas,
más una ley de diseño muy útil.

**Variaciones Protegidas (~50 s)**
Es el patrón paraguas: predecir qué partes van a cambiar y protegerlas detrás de
una interfaz estable, para que el cambio no se propague. En el ejemplo hay
proveedores de temperatura distintos —Google y Microsoft, cada uno con su API—.
En vez de depender de cada API, ponemos un TemperatureAdapter con un método
estable, GetTemperature(); cada proveedor tiene su adaptador. Si entra un
proveedor nuevo, solo agrego un adaptador. Por debajo usa polimorfismo e
indirección: es la síntesis de varios GRASP.

**Ley de Demeter (~40 s)**
Cerramos con una ley práctica: "no hables con extraños". Un objeto no debería
meterse en las tripas de otro. Un Comercio quiere cobrarle a un Cliente. Mal: el
Comercio le pide la Billetera al Cliente y opera sobre ella —queda acoplado a
cómo está hecho el Cliente por dentro—. Bien: el Comercio le pide al Cliente
"pagá este monto", y el Cliente maneja su propia billetera. Menos acoplamiento.

**Cierre (~25 s)**
La idea que se llevan: los nueve GRASP son herramientas para decidir quién hace
qué, pero ninguno se aplica a ciegas. Cohesión es qué tan asociadas están las
responsabilidades de una clase; acoplamiento, qué tan atada está a otras. Todo
GRASP se valida contra esas dos métricas: alta cohesión, bajo acoplamiento.
Muchas gracias, quedamos para las preguntas.

---

### Consejos de ensayo
- Cronometren cada bloque; si se pasan, recorten los ejemplos, no la definición.
- Practiquen las **transiciones** ("le paso a…"): dan continuidad y evitan silencios.
- En modo presentador (`p`) ven estas notas + la próxima diapositiva.
- Ensayen una vez completo para ajustar a la ventana de 15–20 min.
