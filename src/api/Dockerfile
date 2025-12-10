# --- Étape 1 : Build (Compilation) ---
# On utilise Maven avec Java 17 pour construire le projet
# CORRECTION ICI : Utilisation d'une version valide de l'image Maven
FROM maven:3.9-eclipse-temurin-21 AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier le fichier de configuration Maven (pom.xml) et le code source
COPY pom.xml .
COPY src ./src

# Compiler le projet et créer le .jar (skipTests pour aller plus vite comme demandé)
RUN mvn clean package -DskipTests

# --- Étape 2 : Exécution ---
# Image finale légère pour l'exécution
FROM eclipse-temurin:21-jre-alpine

# Créer un répertoire pour stocker la base de données (pour le PVC plus tard)
VOLUME /data

# Copier le fichier .jar généré depuis l'étape de build
# Note: le nom du fichier généré se trouve généralement dans target/
COPY --from=build /app/target/*.jar app.jar

# Commande de lancement
ENTRYPOINT ["java", "-jar", "/app.jar"]