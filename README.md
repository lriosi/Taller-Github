<div align="center">

  # Michelangelo: Machine Learning as a Service Platform en Uber
  
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

1. **Gestión de Datos y Feature Store:**
   * Organización y control de las características para evitar repetir código.
   * Procesa los datos por lotes usando Apache Spark y en tiempo real con Apache Flink y Samza, almacenando la información en Apache Cassandra.
2. **Entrenamiento Distribuido:**
   * Organización de los procesos de trabajo en clústeres distribuidos usando Apache Spark MLlib y Horovod para el aprendizaje profundo.
   * División eficiente de grandes cantidades de datos geoespaciales y transaccionales.
3. **Evaluación de Modelos:**
   * Comparación de modelos candidatos frente a los ya existentes.
   * Generación automática de curvas ROC, matrices de confusión, importancia de variables y métricas de error.
4. **Despliegue de Modelos:**
   * Empaquetado estándar de los modelos y sus procesos de transformación para pasarlos directamente a los clústeres de inferencia sin tener que volver a escribir el código.
5.  **Inferencia y Predicción:**
   * **Inferencia Offline:** Tareas programadas en Apache Spark para realizar muchas predicciones cuando no es necesario obtener resultados rápidamente.
   * **Inferencia Online:** Nodos de servicio de predicción de baja latencia con interfaces RPC.
