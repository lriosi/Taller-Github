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

## Características de ciencia de datos en el proyecto
La ciencia de datos desempeña un papel fundamental en Michelangelo, ya que es la rama encargada de desarrollar y evaluar los modelos de aprendizaje automático que permiten resolver los problemas de negocio.

Podemos identificar siete actividades principales:
1. **Identificar el problema**: Determinar qué se necesita predecir y cuáles son las variables relevantes.
2. **Preparación de los datos**: Seleccionar y transformar los datos de distintas fuentes. También conocido como limpieza de datos.
3. **Ingeniería de características**: Dise4ñar las variables que serán utilizadas en los modelos y almacenarlas.
4. **Entrenamiento**: Seleccionar algoritmos, ajustar los parámetros y llevar a cabo experimentos.
5. **Evaluación**: Analizar méttricas de desempeño y comparar modelos para escoger al que obtenga resultados más precisos y exactos.
6. **Implementación**: Trabajar junto a ingenieros de software y desarrolladores para desplegar los modelos en producción.
7. **Supervisión**: Monitorear la precisión de las predicciones y realizar actualizaciones cuando el rendimiento disminuya.
   <br>
---

## Líderes del Proyecto
* **Jeremy Hermann** - Engineering Manager & Head of Machine Learning Platform en Uber.
* **Mike Del Balso** - Product Manager & Data Product Lead en Uber ML Platform.

---
## Motivación detras de Michelangelo
Antes del desarrollo de Micheangelo, los científicos de datos de Uber utilizaban múltiples herramientas para construir modelos predictivos. No obstante, llevar estos modelos a producción representaba un desafío, pues se requería una solución independiente por proyecto. El desarrollo de esta aplicación permitió centralizar procesos.
---
## Arquitectura y Componentes Clave

El sistema gestiona las 6 etapas del ciclo de vida de Machine Learning:

 1. **Gestión de Datos y Feature Store:**
   * Organización y control de las características para evitar repetir código.
   * Procesa los datos por lotes usando Apache Spark y en tiempo real con Apache Flink y Samza, almacenando la información en Apache Cassandra.
<br>
  <div align="center">
  <img width="2160" height="1230" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy9jMTZjYjdiYy03ZGQzLTU5M2ItYjdmZC1iNTlhZjM4YzczYTAuanBn" src="https://github.com/user-attachments/assets/1bc4015a-51b3-4e9d-b07c-9177ba68cc2c" />  
    Figura 1: Las canalizaciones de preparación de datos envían los datos a las tablas de Feature Store y a los repositorios de datos de entrenamiento.
  </div>
<br>
 2. **Entrenamiento Distribuido:**
   * Organización de los procesos de trabajo en clústeres distribuidos usando Apache Spark MLlib y Horovod para el aprendizaje profundo.
   * División eficiente de grandes cantidades de datos geoespaciales y transaccionales.
     
   <div align="center">
   <img width="2160" height="1237" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy8yMTk2YWFjYy0zNTQ5LTU1ZTAtYTg0OS1mZWRjODQ5ZDg3ZWIuanBn" src="https://github.com/user-attachments/assets/3bd37ae5-f971-4872-84fe-001cc050308d" />
    Figura 2: Los trabajos de entrenamiento de modelos utilizan los conjuntos de datos del repositorio de datos de entrenamiento y de Feature Store para entrenar los modelos y luego enviarlos al repositorio de modelos.
   </div>
   
3. **Evaluación de Modelos:**
   * Comparación de modelos candidatos frente a los ya existentes.
   * Generación automática de curvas ROC, matrices de confusión, importancia de variables y métricas de error.

    <div align="center">
    <img width="2160" height="1063" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy9jYjEzZDBjYS1iZTAwLTVjMGEtOWVhOS00NzI0OWMxY2Q0ZDguanBn" src="https://github.com/user-attachments/assets/1dec5e0c-98e1-4622-b6d6-a1eddf6ed723" />
    Figura 3: Las características, su impacto en el modelo y sus interacciones se pueden explorar a través de un informe de características.
    </div>
    
 4. **Despliegue de Modelos:**
   * Empaquetado estándar de los modelos y sus procesos de transformación para pasarlos directamente a los clústeres de inferencia sin tener que volver a escribir el código.
    
 5.  **Inferencia y Predicción:** 
   * **Inferencia Offline:** Tareas programadas en Apache Spark para realizar muchas predicciones cuando no es necesario obtener resultados rápidamente.
   * **Inferencia Online:** Nodos de servicio de predicción de baja latencia con interfaces RPC.
     
 6. **Monitoreo de Modelos:** 
   * Seguimiento del rendimiento del modelo en producción.
   * Detección de cambios en los datos y pérdida de precisión.
   * Reentrenamiento y actualización cuando el desempeño disminuye.
---
## Caso de uso: Uber Eats
Uno de los casos donde más podemos notar la implementación de Michelangelo es Uber Eats, donde, como se ha mencionado anteriormente, se utilizan modelos de machine learning para estimar el tiempo de preparación y entrega de los pedidos. Esto lo logra gracias a que el sistema realiza las respectivas predicciones antes que el usuario confirme su pedido y las actualiza durante el transcurso del pedido. Para llevar este proceso a cabo, se utilizan tres tipos de información: los datos de la solicitud, los datos históricos y los datos en un tiempo cercano.
 
 <div align="center">
<img width="2160" height="1451" alt="srcb64=aHR0cHM6Ly90Yi1zdGF0aWMudWJlci5jb20vcHJvZC91ZGFtLWFzc2V0cy80ZDgwMzJhMC04ZTI4LTVlZTgtOTg3Ni0xZjU3MTUzMDQ2YmMuanBn" src="https://github.com/user-attachments/assets/bcbe8090-610e-4c3a-9715-95ccead81824" />
   Figura 4: La aplicación UberEATS incluye una función de estimación del tiempo de entrega basada en modelos de aprendizaje automático desarrollados con Michelangelo.
</div>

El modelo utiliza regresión mediante árboles de decisión potenciados por gradiente para estimar el tiempo de entrega. Este módelo permite proporcionar los tiempos estimados.

---
**Referencia**
  * https://www.uber.com/us/en/blog/michelangelo-machine-learning-platform/
  
