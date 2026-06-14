##CRIANDO ARQUIVO DOCKER FILE
#
##importar o maven para fazer o build da aplicação
##from busca imagem do maven   -  build apos vai buildar o maven
#FROM eclipse-temurin:17-jre-alpine AS build
#
##copia para dentro do confainer
#COPY src /app/src
#COPY pom.xml /app
#
##mudar para diretorio /app faz instalações das depndencias
#WORKDIR /app
#RUN mvn clean install
#
##coloca jdk do java no container pega a imagem da AWS tras p dentro do container
#FROM eclipse-temurin:17-jre-alpine
#
##copia
#COPY --from=build /app/target/world-hello-0.0.1-SNAPSHOT.jar /app/app.jar
#
##troca o diretorio
#WORKDIR /app
#
##exponhe a porta que vai abrir
#EXPOSE 8080
#
##faz essa sequencia de comandos no cmd passando por array
#CMD ["java", "-jar", "app.jar"]


# Etapa 1: Build da aplicação com Maven
FROM maven:3.8.4-eclipse-temurin-17 AS build

# Define o diretório de trabalho
WORKDIR /app

# Copia apenas os arquivos necessários para baixar dependências primeiro (melhor para cache)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copia o restante do código-fonte
COPY src ./src

# Compila o projeto e gera o JAR
RUN mvn clean package -DskipTests

# Etapa 2: Imagem final com JRE
FROM eclipse-temurin:17-jre-alpine

# Define o diretório de trabalho
WORKDIR /app

# Copia o JAR gerado da etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Expõe a porta padrão do Spring Boot
EXPOSE 8080

# Comando para iniciar a aplicação
CMD ["java", "-jar", "app.jar"]
