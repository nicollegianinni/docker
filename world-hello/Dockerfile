#CRIANDO ARQUIVO DOCKER FILE

#importar o maven para fazer o build da aplicação
#from busca imagem do maven   -  build apos vai buildar o maven
FROM maven:3.8.4-jdk-8 AS build

#copia para dentro do confainer
COPY src /app/src
COPY pom.xml /app

#mudar para diretorio /app faz instalações das depndencias
WORKDIR /app
RUN mvn clean install

#coloca jdk do java no container pega a imagem da AWS tras p dentro do container
FROM openjdk:8-jre-alpine

#copia
COPY --from=build /app/target/spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar /app/app.jar

#troca o diretorio
WORKDIR /app

#exponhe a porta que vai abrir
EXPOSE 8080

#faz essa sequencia de comandos no cmd passando por array
CMD ["java", "-jar", "app.jar"]