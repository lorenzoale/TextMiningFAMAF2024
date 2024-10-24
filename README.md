# TextMiningFAMAF2024
## Proyecto: Desidentificación en textos de salud

1. Contexto

El Grupo [OMCC](https://www.omcc.lu/) (Online Medical Concept Company), establecido en Luxemburgo, establecido en
Luxemburgo, es una organización que trabaja en el tratamiento del cáncer mediante radioterapia
externa, oncologı́a médica, rayos X de diagnóstico y patologı́a anatómica.
Los servicios técnicos ofrecidos por OMCC abarcan desde la construcción y equipamiento de cen-
tros médicos, hasta el desarrollo y soporte de paquetes de software para la gestión y el ejercicio de
estas actividades clı́nicas. Opera en Europa y en África, con el objetivo de hacer que el tratamiento
oncológico sea accesible a todos los pacientes y con las mismas tecnologı́as.

2. El projecto

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
(CNIL), [cni20] y el Reglamento General de Protección de Datos (RGPD). [rgp].

```bibtex
@article{azzouzi2024automatic,
  title={Automatic de-identification of French electronic health records: a cost-effective approach exploiting distant supervision and deep learning models},
  author={Azzouzi, Mohamed El and Coatrieux, Gouenou and Bellafqira, Reda and Delamarre, Denis and Riou, Christine and Oubenali, Naima and Cabon, Sandie and Cuggia, Marc and Bouzill{\'e}, Guillaume},
  journal={BMC Medical Informatics and Decision Making},
  volume={24},
  number={1},
  pages={54},
  year={2024},
  publisher={Springer}
}
```
