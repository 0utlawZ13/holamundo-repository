# Usa una imagen base de Maven para compilar el proyecto
FROM maven:3.9-eclipse-temurin-17 AS build

# Configura el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia los archivos necesarios para la compilación
COPY pom.xml ./
COPY src ./src

# Ejecuta el comando de Maven para compilar el proyecto
RUN mvn clean package -DskipTests

# Usa una imagen más liviana para ejecutar el JAR
FROM eclipse-temurin:17-jre-alpine

# Configura el directorio de trabajo para la aplicación
WORKDIR /app

# Copia el archivo JAR generado desde la etapa de compilación
COPY --from=build /app/target/*.jar app.jar

# Expone el puerto en el que corre la aplicación (ajusta según tu configuración)
EXPOSE 8080

# Comando para ejecutar el JAR
CMD ["java", "-jar", "app.jar"]
