<div align="center">

  # Michelangelo: Machine Learning as a Service Platform en Uber
  
</div>

<div align="center">
<img width="2304" height="987" alt="image" src="https://github.com/user-attachments/assets/6187d141-5368-4cd5-a0e4-4def246f8505" />
</div>

## Descripción General
  Michelangelo es la plataforma interna de Machine Learning as a Service (MLaaS) desarrollada por Uber, creada para facilitar y organizar el proceso de desarrollo y uso de modelos de aprendizaje automático en producción.

  El proyecto busca conectar los prototipos locales con la implementación de modelos que puedan funcionar en tiempo real y con una baja latencia.

---

## Líderes del Proyecto
* **Jeremy Hermann** - Engineering Manager & Head of Machine Learning Platform en Uber.
* **Mike Del Balso** - Product Manager & Data Product Lead en Uber ML Platform.

---

## Arquitectura y Componentes Clave

El sistema gestiona las 6 etapas del ciclo de vida de Machine Learning:

<h2> 1. **Gestión de Datos y Feature Store:** </h2>
   * Organización y control de las características para evitar repetir código.
   * Procesa los datos por lotes usando Apache Spark y en tiempo real con Apache Flink y Samza, almacenando la información en Apache Cassandra.
     
  <div align="center">
  <img width="2160" height="1230" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy9jMTZjYjdiYy03ZGQzLTU5M2ItYjdmZC1iNTlhZjM4YzczYTAuanBn" src="https://github.com/user-attachments/assets/1bc4015a-51b3-4e9d-b07c-9177ba68cc2c" />  
    Figura 1: Las canalizaciones de preparación de datos envían los datos a las tablas de Feature Store y a los repositorios de datos de entrenamiento.
  </div>


<h2> 2. **Entrenamiento Distribuido:**</h2>
   * Organización de los procesos de trabajo en clústeres distribuidos usando Apache Spark MLlib y Horovod para el aprendizaje profundo.
   * División eficiente de grandes cantidades de datos geoespaciales y transaccionales.
     
    <div align="center">
    <img width="2160" height="1237" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy8yMTk2YWFjYy0zNTQ5LTU1ZTAtYTg0OS1mZWRjODQ5ZDg3ZWIuanBn" src="https://github.com/user-attachments/assets/3bd37ae5-f971-4872-84fe-001cc050308d" />
    Figura 2: Los trabajos de entrenamiento de modelos utilizan los conjuntos de datos del repositorio de datos de entrenamiento y de Feature Store para entrenar los modelos y luego enviarlos al repositorio de modelos.
    </div>

<h2> 3. **Evaluación de Modelos:** </h2>
   * Comparación de modelos candidatos frente a los ya existentes.
   * Generación automática de curvas ROC, matrices de confusión, importancia de variables y métricas de error.

    <div align="center">
    <img width="2160" height="1063" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy9jYjEzZDBjYS1iZTAwLTVjMGEtOWVhOS00NzI0OWMxY2Q0ZDguanBn" src="https://github.com/user-attachments/assets/1dec5e0c-98e1-4622-b6d6-a1eddf6ed723" />
    Figura 3: Las características, su impacto en el modelo y sus interacciones se pueden explorar a través de un informe de características.
    </div>
    
<h2> 5. **Despliegue de Modelos:** </h2>
   * Empaquetado estándar de los modelos y sus procesos de transformación para pasarlos directamente a los clústeres de inferencia sin tener que volver a escribir el código.
    
<h2> 7.  **Inferencia y Predicción:** </h2>
   * **Inferencia Offline:** Tareas programadas en Apache Spark para realizar muchas predicciones cuando no es necesario obtener resultados rápidamente.
   * **Inferencia Online:** Nodos de servicio de predicción de baja latencia con interfaces RPC.
     
<h2> 6. **Monitoreo de Modelos:** </h2>
   * Seguimiento del rendimiento del modelo en producción.
   * Detección de cambios en los datos y pérdida de precisión.
   * Reentrenamiento y actualización cuando el desempeño disminuye.

**Caso de uso: Uber Eats**
Uno de los casos donde más podemos notar la implementación de Michelangelo es Uber Eats, donde, como se ha mencionado anteriormente, se utilizan modelos de machine learning para estimar el tiempo de preparación y entrega de los pedidos. Esto lo logra gracias a que el sistema realiza las respectivas predicciones antes que el usuario confirme su pedido y las actualiza durante el transcurso del pedido. Para llevar este proceso a cabo, se utilizan tres tipos de información: los datos de la solicitud, los datos históricos y los datos en un tiempo cercano.
 
 <div align="center">
<img width="2160" height="1451" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy80ZDgwMzJhMC04ZTI4LTVlZTgtOTg3Ni0xZjU3MTUzMDQ2YmMuanBn" src="https://github.com/user-attachments/assets/bcbe8090-610e-4c3a-9715-95ccead81824" />
   Figura 5: La aplicación UberEATS incluye una función de estimación del tiempo de entrega basada en modelos de aprendizaje automático desarrollados con Michelangelo.
</div>

El modelo utiliza regresión mediante mediante árboles de decisión potenciados por gradiente para estimar el tiempo de entrega. Este módelo permite proporcionar los tiempos estimados.

**Ciencia de datos en el proyecto**



**Referencia**
  * https://www.uber.com/us/en/blog/michelangelo-machine-learning-platform/
  
