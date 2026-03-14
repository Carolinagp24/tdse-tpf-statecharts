<p align="center">
  <img src="./img/logo-fiuba.png" alt="image1">
</p>

<p align="center">
  <strong>UNIVERSIDAD DE BUENOS AIRES</strong>
</p>

<p align="center">
  <strong>Facultad de Ingeniería</strong>
</p>

<p align="center">
  <strong>86.65/TA134 Taller de Sistemas Embebidos</strong>
</p>

# Memoria del trabajo final: **Alarma vecinal**

<table align="center">
  <tr>
    <th>Autor</th>
    <th>Padrón</th>
  </tr>
  <tr>
    <td>Valentín Alexis Guirin</td>
    <td>107416</td>
  </tr>
  <tr>
    <td>Yerson Monzón Alayo</td>
    <td>104262</td>
  </tr>
  <tr>
    <td>Carolina Gonzales Peralta</td>
    <td>110804</td>
  </tr>
</table>

<p align="center">
  <em>Este trabajo fue realizado en la Ciudad Autónoma de Buenos Aires, entre diciembre de 2025 y marzo de 2026.</em>
</p>

# RESUMEN
En el presente trabajo se diseñó e implementó una alarma vecinal. Se pretendía solucionar la problemática de inseguridad en barrios comprometidos de la Ciudad de Buenos Aires o sus alrededores.
Mediante un módulo GSM y un botón de pánico se logró que los usuarios puedan hacer sonar una alarma sonora y con luz estroboscópica para notificar a la policía y a la central inmediatamente. Para su mantenimiento, un vecino encargado puede conectarse a través del módulo BLE con doble factor de autenticación.
La importancia de este trabajo radica en la consolidación de lo aprendido en la materia en cuestión en un trabajo integral de este calibre, además de solucionar potencial y parcialmente el problema de la inseguridad ya mencionado. El actual trabajo es una buena representación de lo aprendido durante la cursada del Taller de Sistemas Embebidos ya que involucra el manejo de la placa STM para comunicar módulos entre sí, vinculando así la implementación de un código con la interconexión de los distintos elementos que componen al sistema.
En esta Memoria se encontrará la motivación del proyecto, diseños de partes y la propuesta de posibles mejoras a implementar.

# ABSTRACT
This paper describes the design and implementation of a neighborhood alarm system aimed at addressing security concerns in high-risk areas of the City of Buenos Aires. By utilizing a GSM module and a panic button, users can trigger an audible alarm and a strobe light to notify both the neighborhood and a central station. For maintenance purposes, technicians can connect via a BLE (Bluetooth Low Energy) module using their personal credentials.
The significance of this project lies in the consolidation of the knowledge acquired throughout the course into a comprehensive technical application, while offering a potential solution to the aforementioned security issues. This project serves as a robust representation of the learning outcomes from the Embedded Systems course, as it involves programming an STM board to manage inter-module communication, effectively linking software implementation with the interconnection of diverse hardware components.
This report details the project’s motivation, component designs, and proposes future enhancements.

# Agradecimientos
Agradecemos, como grupo, al Ingeniero Juan Manuel Cruz por el tiempo dedicado a ayudarnos con el desarrollo del proyecto en tiempo real, ya sea desde responder consultas en cualquier momento a personalmente intervenir en las complicaciones tan específicas que fueron surgiendo en todo momento.
También, al Dr. Ingeniero Ariel Lutenberg, por su impecable predisposición en todo momento para solucionarnos cualquier consulta referida a cualquier cuestión por más técnica y específica que sea, y por estar atento a hacernos el proceso de generar el proyecto final mucho más ameno de lo que podría haber sido.
A ambos les agradecemos por la motivación genuina por los sistemas embebidos que han  generado en nosotros como estudiantes de Ingeniería Electrónica, haciendo que un proyecto con tiempos de entrega determinados y un examen con su intrínseca burocracia detrás, se vuelva algo placentero de transitar.

# Índice general
- [Agradecimientos](#agradecimientos)	
- [Registro de versiones](#registro-de-versiones)
- [Introducción general](#introducción-general)
 - [1.1 Problemática a resolver](#11-problemática-a-resolver)	
 - [1.2 Solución a implementar](#12-solución-a-implementar)
 - [1.3 Análisis de sistemas similares al desarrollado](#13-análisis-de-sistemas-similares-al-desarrollado)
- [Introducción específica](#introducción-específica)
 - [2.1 Requisitos](#21-requisitos)
 - [2.2 Casos de uso]	
 - [2.3 Descripción  módulos del sistema]
  - [2.3.1 Alimentación]	
  - [2.3.2 Microcontrolador]	
  - [2.3.3 Módulo GSM]
  - [2.3.4 Memoria EEPROM AT24C256]
  - [2.3.5 Módulo Bluetooth]	
2.3.6 Módulo sensor de luz	
2.3.7 Indicadores	
2.3.8 Aplicación de celular	
2.3.9 Conexionado	
- [Diseño e implementación]
 - [3.1 Diseño del Hardware]
3.1.1 Hardware del módulo GSM	21
3.1.2 Hardware del módulo HM-10	23
3.1.3 Hardware del módulo sensor de luz LDR	
3.1.4 Hardware de la memoria EEPROM AT24C256	
 - [3.2 Diseño del Firmware	]
3.2.1 Main	
3.2.2 Botón de pánico	
3.2.3 Sensor de luz	
3.2.4 Módulo Bluetooth	
3.2.5 Módulo GSM	
3.2.6 Gestión de mensajes SMS	
- [Ensayos y resultados]	
4.1 Desarrollo y pruebas de funcionamiento	
4.2 Cumplimiento de requisitos	
4.3 Análisis de Ejecución y Consumo Energético	
4.3.1 Medición y análisis de consumo	
4.3.1.1 Análisis del módulo GSM (SIM800L)	
4.3.2 Medición y análisis de tiempos de ejecución de cada tarea (WCET)	
4.3.2.1 Análisis Matemático y Conversión Temporal:	
4.3.3 Captura de pantalla de "Console & Build Analyzer"	
4.3.4 Cálculo del Factor de Uso (U) de la CPU	
4.3.5 Gestión del modo de bajo consumo	
 - [4.4 Documentación del desarrollo realizado]
- [Conclusiones]
5.1 Resultados obtenidos	
5.2 Próximos pasos	
- [Uso de herramientas de la inteligencia artificial.]
6.1 Uso individual	
- [Bibliografía]

# Registro de versiones

| Revisión | Cambios realizados | Fecha |
| --- | --- | --- |
| 1.0 |Creación del documento | 24/02/2026 |
| 1.1 | Agregado de capítulos 1 y 2 |  24/02/2026 |
| 1.2 | Agregado parcial de capítulo 3 | 25/02/2026 |
| 1.3 | Capítulo 3 completo y parcialmente el capítulo 4 | 26/02/2026|
| 1.4 | Terminado el documento | 27/02/2026 |
| 1.5 | Versión final con detalles corregidos | /03/2026 |

# CAPÍTULO 1 
# Introducción general
## 1.1 Problemática a resolver
En la realidad de hoy en día y en el contexto de la Ciudad Autónoma de Buenos Aires, la inseguridad se ha vuelto un problema a tener en cuenta mayormente a medida que pasan los años. Si bien el problema trasciende en toda la ciudad, sería imprudente no destacar que la problemática en cuestión tiene un mayor impacto y se ve con mayor frecuencia en las llamadas “villas” alrededor de la ciudad.
Según estadísticas de la página de la Ciudad de Buenos Aires, las comunas en donde más delitos se presentan son en aquellas en las que hay villas. Particularmente, en la Comuna 1 es en la que más delitos hubo en diciembre de 2024 y en la que se asienta la Villa 31, la más poblada de la ciudad. En la Figura 1.1 se detalla la distribución de delitos por comuna.


Nuestro proyecto fue pensado para instalarse en las villas, en donde la comunidad barrial pueda unirse y organizarse. La idea fue crear un dispositivo que cualquier vecino pueda alertar a todo el barrio, aprovechando que una sola persona puede hacer que todos reaccionen.
El hecho de que sea un producto aplicado a este tipo de zonas, viene también de la mano con el personal policial disponible para tanta área. Al no tener la ciudad el presupuesto para poner mayor cantidad de personal de seguridad en cada esquina de las villas, la única opción viable es que los habitantes se cuiden entre sí, y es por eso que nuestra alarma vecinal fue diseñada para combatir los hechos delictivos aislados por el bajo control policial, haciendo de la red de vecinos una red segura y menos atractiva para quienes delinquen.
El hecho de haber elegido las villas como mercado fue producto de reconocer que son las zonas de la ciudad con menor seguridad disponible y de entender que las zonas más urbanizadas de la ciudad son mucho más seguras y ya hay soluciones mucho menos sofisticadas que cumplen perfectamente la función de cuidar a los vecinos.
## 1.2 Solución a implementar
La solución al problema de la inseguridad en las villas no se soluciona exclusivamente con una alarma vecinal, pero sí se puede reducir considerablemente la costumbre delictiva que está presente y en crecimiento en esas partes de la ciudad.
Nuestro producto fue pensado y diseñado para ahuyentar y alertar. Posee un botón de pánico accesible para cualquier persona que esté pasando por una situación de inseguridad o para cualquier testigo de alguna. La funcionalidad que fue añadida pensando en los posibles escenarios de delincuencia fue la posibilidad de que algún vecino realice una llamada al número asociado a la alarma y active la alarma remotamente. Esto fue implementado debido a que muchas situaciones delictivas se ven, pero no se enfrentan por miedo a involucrarse. De esta manera, creemos que haber implementado la funcionalidad mencionada, hará que muchas acciones delictivas puedan frenar antes de tiempo o mitigar sus efectos.
Además, la alarma vecinal posee una luz estroboscópica y alarma sonora. Ambas son para alertar al vecindario y ahuyentar al delincuente. La luz únicamente se prende si hay muy baja iluminación, ya que sino sería un gasto de recursos sin sentido. Cabe destacar que al tener como prioridad que se cree una red segura entre vecinos, los usuarios habilitados para llamar son exclusivamente miembros de la calle donde está instalada esta y deben ser incluidos en una whitelist que genera la central. Al momento de la instalación, el técnico podrá conectarse vía Bluetooth a la alarma con su usuario y contraseña y cargar esa lista. Privilegios de administrador serán otorgados a miembros específicos de cada comunidad para poder agregar o quitar miembros de esa lista, para así afianzar todavía más la confianza entre la red del barrio.
## 1.3 Análisis de sistemas similares al desarrollado
Existen empresas como Global Alarmas [2], Hexacom [3], Alerta Vecinal [4], Safecity [5] y Verisure [6] que ofrecen a grandes rasgos lo mismo que nuestra solución. Habiendo más de un competidor, fue importante para nosotros pensar en alguna característica distintiva que destaque entre las demás. El carácter de red vecinal profunda que promete nuestro producto es, en parte, lo que hace que nuestra alarma vecinal no solo sea una herramienta, sino un símbolo de seguridad comunitaria. 
Entre algunas de las funcionalidades que se ofrecen por estas empresas en sus productos se encuentran: sirena de luz, alerta sonora, botonera y panel de control, rastreo vehicular, emisores de humo denso, whitelist, aplicación móvil y control remoto, entre otras.
Cabe mencionar que solo una de estas empresas, Alerta Vecinal, está dedicada exclusivamente al desarrollo de alarmas para comunidades y no para domicilios particulares.
Si bien ya existen alarmas con listas tipo whitelist, nuestro concepto de whitelist descentralizada (que usuarios dentro de la red puedan operar con ella) hace que el sentimiento de comunidad sea más fuerte si se elige nuestra propuesta, además de que la construcción y mantenimiento de la alarma es muy baja. Se suma el hecho de que se puede reportar un acto ilícito de manera silenciosa y anónima mediante una llamada telefónica, solo la central sabrá qué número de la whitelist activó la alarma. Muchas alarmas ofrecen protección exclusivamente a uno mismo, mientras que nosotros brindamos la posibilidad de cuidarnos entre todos.
Por otro lado, el uso de la interfaz Bluetooth para el vecino encargado es un enfoque moderno y que facilita la instalación y mantenimiento de alarmas en puntos estratégicos y peligrosos, ya que a veces puede ser complicado operar en ciertos puntos.
Por último, el sensor de luz no es un detalle menor, ya que con esa simple incorporación el barrio consume electricidad para la iluminación únicamente cuando es necesario, y eso se ve reflejado en ahorros de energía eléctrica considerables.

# CAPÍTULO 2 
# Introducción específica
## 2.1 Requisitos
En la Tabla 2.1 se detalla la lista de requisitos a cumplimentar, con el objetivo de desarrollar un dispositivo que pueda cumplir con lo especificado en la Sección 1.2.

