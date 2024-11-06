# TextMiningFAMAF2024
## Proyecto: Desidentificación en textos de salud

## 1. Contexto

El Grupo [OMCC](https://www.omcc.lu/) (Online Medical Concept Company), establecido en
Luxemburgo, es una organización que trabaja en el tratamiento del cáncer mediante radioterapia
externa, oncologı́a médica, rayos X de diagnóstico y patologı́a anatómica.
Los servicios técnicos ofrecidos por OMCC abarcan desde la construcción y equipamiento de cen-
tros médicos, hasta el desarrollo y soporte de paquetes de software para la gestión y el ejercicio de
estas actividades clı́nicas. Opera en Europa y en África, con el objetivo de hacer que el tratamiento
oncológico sea accesible a todos los pacientes y con las mismas tecnologı́as.

## 2. El projecto

En el campo de la oncologı́a, el procesamiento del lenguaje natural (PLN) desempeña un papel muy
importante en la extracción de información valiosa. En este contexto, aparecen varios campos de
trabajo que pueden ayudar a mejorar la atención sanitaria. Por ejemplo podriamos pensar en utilizar
el reconocimiento de entidades nombradas (NER) y la extracción de información, para ayudar en
la identificación de regiones/grupos que desarrollan tumores especı́ficos. Esta información se puede
obtener a partir de los datos existentes en los centros de tratamiento, en particular de los informes
patológicos existentes. Por ejemplo, en la Imagen siguiente mostramos el ejemplo de un caso de cáncer de
mama. A la izquierda podemos ver el formulario de diagnóstico y a la derecha la última página
del documento de patologı́a correspondiente. Los colores representan la alineación entre el texto del
documento de patologı́a y los campos que corresponden a este texto en el formulario de diagnóstico.

![Imagen 1](/img/exemple_syst.jpg)

Además, en este conjunto de datos cada paciente tiene asociada su dirección y otra información, de
la que podrı́amos extraer, de forma anonimizada, la región y/o otra información del grupo que serı́a
de ayuda para identificar clusters vulnerables.
Sin embargo, el uso de datos de salud, que contienen información personal identificable (PII) sobre
pacientes y médicos, plantea un gran desafı́o en términos de seguridad y confidencialidad. Hace falta
preservar la privacidad de los pacientes y, por lo tanto, proponemos en este proyecto trabajar en la
desidentificación. Desidentificación es el proceso de eliminar información identificable de los datos.
Existen diferentes niveles de desidentificación. En su nivel más básico, consiste en eliminar u ocultar
información como el nombre de la persona, la fecha de nacimiento, el sexo o la dirección. Pero más
allá de este nivel básico, podrı́amos utilizar otras informaciones para volver a identificar a alguien con
bastante facilidad (con un poco de trabajo adicional). Por ejemplo, la dirección IP de alguien o el ID
único del dispositivo asociado con su marcapasos, etc.
Estados Unidos fue el primero en definir las entidades que se deberı́an eliminar según la Ley de
Portabilidad y Responsabilidad del Seguro Médico (Health Insurance Portability and Accountability
Act, HIPAA). El proceso de desidentificación baja los riesgos de privacidad de las personas y, por lo
tanto, respalda el uso secundario de los datos para estudios de efectividad comparativa, evaluación de
polı́ticas, investigación en ciencias de la vida y otros esfuerzos [PA12].
La Ley de Portabilidad y Responsabilidad de Seguros Médicos (HIPAA) identifica 18 entidades de
identificación directa (DIE).

1. Números de fax
2. Direcciones de correo electrónico
3. Números de seguro social
4. Números de registros médicos
5. Números de beneficiarios de seguros médicos
6. Números de cuenta
7. Números de certificado/licencia
8. Identificadores de vehı́culos
9. Atributos o números de serie del dispositivo
10. Identificadores digitales, como URL de sitios web
11. Direcciones IP
12. Elementos biométricos, incluidas huellas dactilares, retinianas y de voz
13. Imágenes fotográficas de rostro completo
14. Otros números o códigos de identificación

En Francia, para garantizar la protección de la confidencialidad de los datos personales en los
registros médicos electrónicos, es necesario cumplir con las regulaciones gubernamentales establecidas
por la Autoridad de Protección de Datos francesa, la Comisión Nacional de Informática y Libertades
(CNIL) [[1]](#1) y el Reglamento General de Protección de Datos (RGPD) [[2]](#2) . 

Cualquier proyecto que utilice datos sanitarios debe ser examinado por el comité científico y ético nacional (CESREES) antes de ser confiado a la CNIL. 
Para esto en el sitio de Health data hub se provee un starter kit (https://www.health-data-hub.fr/starter-kit). En el se establecen las siguientes condiciones: 

- En primer lugar, mi proyecto debe perseguir un propósito de interés público. Esto no es a priori incompatible con una actividad comercial pero tiene que quedar explicado en el protocolo.
- En segundo lugar, debo solicitar la autorización de la CNIL, salvo en casos muy específicos en los que mi estudio pueda acogerse a procedimientos derogatorios o simplificados. En este caso, puedo realizar mi proyecto en el marco de una metodología de referencia (MR).

Una de esas MR se aplica en el caso en el que quiero reutilizar datos de salud existentes y tengo la capacidad de informar individualmente a las personas interesadas antes de implementar mi estudio, la MR 004. Sin embargo, se me prohibirá, por ejemplo:
- recopilar datos personales;
- Realizar un cotejo con otra fuente;
- Utilizar datos SNDS que aún no estén encadenados en una fuente de datos de terceros.



## 2.1. Estado del arte

En [[3]](#3) los autores ofrecen un estudio sobre la evolución de la desidentificación para textos
clı́nicos en inglés durante los últimos trece años. Afirman que los enfoques anteriores eran principal-
mente hı́bridos, basados en reglas y aprendizaje automático, con mucha ingenierı́a de caracterı́sticas
y posprocesamiento. También afirman que las mejoras de rendimiento recientes se deben a redes neu-
ronales recurrentes de inferencia de caracterı́sticas, alcanzando resltados de F1 del estado del arte (más
del 98 %). Sin embargo, destacan la necesidad de más datos anotados para generalizar mejor en la
amplia gama de subdominios clı́nicos.

En [[4]](#4) Los autores presentan un framework de desidentificación basado en GPT4 (“DeID-
GPT”) para identificar y eliminar automáticamente la información de identificación. Sin embargo, a
pesar de sus impresionantes resultados, debido al uso de ChatGPT con API en lı́nea, su sistema no
se puede aplicar en un entorno hospitalario ya que los datos del paciente no se pueden almacenar ni
transmitir a una parte externa no autorizada. Además, resaltan la necesidad de utilizar LLM de código
abierto o capacitados internamente para esta tarea (en lugar de GPT4 ya que su código no está abierto
al público), para garantizar la seguridad, la privacidad, la integridad y el cumplimiento adecuado de
las pautas HIPAA.

[[5]](#5) propone un proceso automatizado y certificado de desidentificación de textos clı́nicos de
la Universidad de California, San Francisco (UCSF), que cumple con la regla de privacidad de la Ley de
Portabilidad y Responsabilidad de Seguros Médicos (HIPAA) para los estándares de desidentificación.
El desarrollo y la auditorı́a de la herramienta llevaron varios años. Los textos clı́nicos desidentificados
certificados están disponibles para la comunidad de investigación de la UCSF sin necesidad de ninguna
otra aprobación de las Juntas de Revisión Institucional (IRB). Sin embargo, todavı́a hay algunos req-
uisitos de acceso vigentes. Continúan con el desarrollo activo para mejorar los problemas de redacción
o las mejoras. Además, para seguir cumpliendo con la HIPAA, el proceso de desidentificación y los
datos deben certificarse cada 2 años.

Algunas iniciativas para la desidentificación automática en francés incluyen la herramienta Medina
(gratuita) [[6]](#6) y la herramienta ALADIN (propietaria) [[7]](#7), dos herramientas basadas
en reglas. En[[8]](#8), los autores proponen un método hı́brido de desidentificación evaluado en
una muestra de textos del conjunto de datos de los servicios de salud de la Assistance Publique
des Hôpitaux de Paris. Combinan reglas, bases de conocimiento y redes neuronales. Sin embargo, la
naturaleza personal de los datos hace necesario configurar un conjunto de datos anotados e imposibilita
la publicación del modelo aprendido. En un enfoque hı́brido similar, más recientemente, en [[9]](#9),
los autores proponen un proceso de desidentificación automática para todo tipo de documentos clı́nicos
basado en un método supervisado a distancia. La limitación de este estudio es que entrenan el modelo
en un corpus de un solo hospital, lo que puede resultar en una falta de generalización.

## 2.2 Propuesta
Datos a desidentificar:
1. Nombres y apellidos del paciente
2. Fecha de nacimiento
3. Fecha de consulta
4. Otras fechas?
5. Nombres y apellidos de médicos
6. Números de telefono y de fax
7. Direcciones de correo electrónico
8. Números de seguro social
9. Números de registros médicos
10. Direcciones: calle, ciudad, codigo postal.
11. Identificadores sobre la consulta
12. Números identificación del paciente
13. Centro de salud (hospitales y centros de anatomopalogia)
Dado que tenemos datos de los pacientes como nombre, apellido, fecha de nacimiento, etc para
cada uno de los reportes, una idea seria usar un metodo basado en reglas (por ejemplo con expresiones
regulares) que pueda detectar estas entidades.

Además, de una manera similar a la propuesta en [[9]](#9), seria bueno usar datos del gobierno
sobre los medicos y centros de salud que figuren como entidades.
Sin embargo, para obtener el texto correspondiente al informe patológico, primero hay que utilizar
un OCR sobre los documentos escaneados. Este paso previo es muy propenso a introducir errores, en
particular cuando los distintos documentos escaneadas presentan mucha diferencia de calidad. Estos
errores hacen que las reglas a aplicar no sean tan efectivas. Para mejorar este problema una opción
es hacer corrección de errores como preprocesamiento, y/o aplicar en conjunto un metodo estadistico.
En la bibliografia combinan métodos estadisticos con reglas. Se pueden pensar en varias opciones para
esto:
1. Un enfoque similar al de [[9]](#9) seria usar reglas para anotar datos y luego usar estos datos
anotados para entrenar un metodo estadistico.
2. Otro enfoque podria ser hacer etapas donde aplicamos primero reglas y luego un método estadis-
tico.

## 2.3 Planificación Inicial
1. Hacer un preprocesamiento o curage de datos sobre los reportes patológicos: tokenizar, probar
sacar “stop words” o no.
2. Definir reglas para identificar las posibilidades de variaciones del nombre de los pacientes, fecha
de nacimiento, dirección, etc.
3. Obtener base de datos de medicos y centros de salud del pais correspondiente.
4. Definir reglas para buscar información de los médicos y centros de salud previamente definidos.
5. Podemos usar métodos/modelos de NER existentes para extraer entidades. Dependiendo de los
modelos las entidades que podemos obtener. Probar distintos modelos.
6. Hacer fine tunning con los datos extraidos de las reglas y obtener nuevas entidades?
7. Anotación: parte de la anotación es con las reglas y/o algoritmo de NER elegido. Pero para
visualizar los resultados una herramienta de anotación es de mucha ayuda. La herramienta
elegida debe ejecutarse en local debido a la privacidad de los datos. Además seria bueno que
tenga licencia de software libre. Una que comencé a explorar hace un tiempo (no en mucho
detalle) es Inception [], TODO: ver otras.Doccano??
8. Evaluación: Las métricas de evaluación elegidas son: Exactitud, Precisión, Sensibilidad y F1
score.

## 2.3 Comentarios de otros grupos
1. Pregunta: ¿Por qué trabajan sobre el documento escaneado y no la versión original digital?. 

Respuesta: El procedimiento estándar es el siguiente: luego de ser diagnosticado, el paciente llega al centro de radioterapia con su reporte patológico y otros estudios médicos en forma de papel. Este papel es escaneado e incorporado al sistema. En general este tipo de reportes no se mandan por mail de forma digital.

2. Pregunta: Siendo el caso que van a definir reglas, ¿consideraron probar algún algoritmo de minado de reglas que les pueda simplificar la tarea?

Respuesta: Muchas gracias, es una opción a considerar pero dado las restricciones de tiempo, como trabajo futuro. Por el momento las reglas son bastantes simples y lo que funciona mejor es combinarlas con métodos estadísticos.

3. Pregunta: ¿Pensaron en evaluar si los datos desidentificados afectan el desempeño a la hora de identificar regiones/grupos que desarrollan tumores específicos?

Respuesta: La idea es extraer "regiones" más que lugares específicos, teniendo en cuenta un número mínimo por regiones para evitar la posible identificación en casos muy específicos.

4. Pregunta: Por ahí faltaría dar más información de los datos a utilizar, el formato y si es necesario realizar algún tipo de preprocesamiento.

Respuesta: Los datos a utilizar corresponden al texto extraído por el OCR de los reportes patológicos de los pacientes. Además, podemos usar el nombre, fecha de nacimiento, dirección, y médicos asociados a cada paciente para asegurarse que el nombre no aparece en el texto desidentificado. Un ejemplo tomado de internet de un reporte patologico:

![Imagen 2](/img/info21.png)
![Imagen 3](/img/info1.png)

5. Pregunta: Con respecto a la curación de datos, tendría cuidado al momento de decidir que es un “stop word”, ya que el tema del proyecto es sobre la medicina, quizás desde un lado de minería de datos se puedan escapar o mal interpretar palabras que sí son útiles.

Respuesta: Definitivamente hace falta un preprocesamiento. En primera instancia al utilizar un OCR haría falta un corrector ortográfico. Además una tokenización. Se consideró la eliminación de stop words pero se descartó la idea como sugerido por los comentarios.


## 2.4 Avances y replanificación

1. **Hecho**: El curage de datos hecho depende mucho de las herramientas posteriores.
En todos los casos se uso un eliminado de blancos extras. Se probo tokenizacion con Spacy pero solo es util cuando se usan reglas.
Se elimino la hipotesis de sacar las "stop words" porque como mencionado en los comentarios puede interferir luego en la fase de extraccion de datos.

2. **Hecho**: Se uso el nombre, fecha de nacimiento y dirección de los pacientes (la información se la puede sacar del sistema). Y se buscó esta información en los textos. 
Sin embargo dado que los textos traen mucho ruido que proviene del OCR, en una evaluación anecdótica se vió que no es suficiente.  

3. **Postergado**: Obtener base de datos de medicos y centros de salud del pais correspondiente es algo a probar posteriormente por falta de tiempo. 

4. **Postergado**: Idem anterior

5. **Hecho**: Método existente de anonymizacion utilizado: [EDS-Pseudo](https://github.com/aphp/eds-pseudo) [[10]](#10). 
También se usó [Presidio](https://microsoft.github.io/presidio/tutorial/11_custom_anonymization/), una herramienta muy utilizada para deidentificación. Se trata de una libreria de NLP open-source desarrollada por Microsoft. En este caso se utilizaron patrones combinados con el método adaptado para usar Transformers (que consiste de un pipeline spaCy que encapsula un modelo de HuggingFace). 
Presidio es una herramienta muy completa. Sin embargo haría falta continuar probando reglas y combinaciones de reglas y métodos estadísticos, dado que en una comparación anecdótica con el método estadístico EDS-Pseudo, este último muestra mejor rendimiento.

Ejemplo de resultado obtenido: ![Imagen 4](/img/aphpEx.png)

7. **Se deja como trabajo futuro por falta de tiempo**  Hacer fine tunning con los datos extraídos de las reglas y obtener nuevas entidades. Sería interesante utilizar la herramienta que mejor resulte en la evaluación para generar datos anotados y utilizar estos datos para hacer fine tuning sobre el modelo EDS-Pseudo [[10]](#10). 

8. **A implementar entre 01/11 y el 01/12** Anotación: Hacer la anotación de un pequeño test set para la evaluación.

9. **Postergado**:  Evaluación: nos quedamos con la evaluación anecdótica dado que los resultados obtenidos se pueden apreciar muy fácilmente y no se considera útil en este nivel hacer una evaluación más profunda.  

10. **Continuacion del proyecto: generación de datos sintéticos**.


## References
<a id="1">[1]</a> L’anonymisation de données personnelles, 2020.

<a id="2">[2]</a> Data protection in the eu.

<a id="3">[3]</a> Aleksandar Kovačević, Bojana Bašaragin, Nikola Milošević, and Goran Nenadić. De-
identification of clinical free text using natural language processing: A systematic review
of current approaches. Artificial Intelligence in Medicine, page 102845, 2024.

<a id="4">[4]</a> Zhengliang Liu, Yue Huang, Xiaowei Yu, Lu Zhang, Zihao Wu, Chao Cao, Haixing Dai,
Lin Zhao, Yiwei Li, Peng Shu, et al. Deid-gpt: Zero-shot medical text de-identification by
gpt-4. arXiv preprint arXiv:2303.11032, 2023.

<a id="5">[5]</a> Lakshmi Radhakrishnan, Gundolf Schenk, Kathleen Muenzen, Boris Oskotsky, Habibeh
Ashouri Choshali, Thomas Plunkett, Sharat Israni, and Atul J Butte. A certified de-
identification system for all clinical text documents for information extraction at scale.
JAMIA open, 6(3):ooad045, 2023.

<a id="6">[6]</a> Cyril Grouin, Arnaud Rosier, Olivier Dameron, and Pierre Zweigenbaum. Une procédure
d’anonymisation à deux niveaux pour créer un corpus de comptes rendus hospitaliers. In
Risques, technologies de l’information pour les pratiques médicales, pages 23–34. Springer,
2009.

<a id="7">[7]</a> Quentin Gicquel, Denys Proux, Pierre Marchal, Caroline Hagége, Yasmina Berrouane,
Stéfan J Darmoni, Suzanne Pereira, Frédérique Segond, and Marie-Héléne Metzger.
Évaluation d’un outil d’aide á l’anonymisation des documents médicaux basé sur le traite-
ment automatique du langage naturel. In Systèmes d’information pour l’amélioration de
la qualité en santé, pages 165–176. Springer, 2011.

<a id="8">[8]</a> Nicolas Paris, Matthieu Doutreligne, Adrien Parrot, and Xavier Tannier. Désidentification
de comptes-rendus hospitaliers dans une base de données omop. In TALMED 2019: Sym-
posium satellite francophone sur le traitement automatique des langues dans le domaine
biomédical, 2019.
<a id="9">[9]</a> Mohamed El Azzouzi, Gouenou Coatrieux, Reda Bellafqira, Denis Delamarre, Christine
Riou, Naima Oubenali, Sandie Cabon, Marc Cuggia, and Guillaume Bouzillé. Automatic
de-identification of french electronic health records: a cost-effective approach exploiting
distant supervision and deep learning models. BMC Medical Informatics and Decision
Making, 24(1):54, 2024.

<a id="10">[10]</a> Xavier Tannier  , Perceval Wajsbürt , Alice Calliger  , Basile Dura  , Alexandre Mouchet , Martin Hilka and Romain Bey. 
Development and Validation of a Natural Language Processing Algorithm to Pseudonymize Documents in the Context of a Clinical Data Warehouse. 
Methods of Information in Medicine. 2024. 
