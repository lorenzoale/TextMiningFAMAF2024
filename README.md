# TextMiningFAMAF2024
## Proyecto: Desidentificación en textos de salud

## 1. Contexto

El Grupo [OMCC](https://www.omcc.lu/) (Online Medical Concept Company), establecido en Luxemburgo, establecido en
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


## References
<a id="1">[1]</a> L’anonymisation de données personnelles, 2020.

<a id="2">[2]</a> Data protection in the eu.

<a id="3">[3]</a> Aleksandar Kovačević, Bojana Bašaragin, Nikola Milošević, and Goran Nenadić. De-
identification of clinical free text using natural language processing: A systematic review
of current approaches. Artificial Intelligence in Medicine, page 102845, 2024.

<a id="4">[4]</a> Zhengliang Liu, Yue Huang, Xiaowei Yu, Lu Zhang, Zihao Wu, Chao Cao, Haixing Dai,
Lin Zhao, Yiwei Li, Peng Shu, et al. Deid-gpt: Zero-shot medical text de-identification by
gpt-4. arXiv preprint arXiv:2303.11032, 2023.
