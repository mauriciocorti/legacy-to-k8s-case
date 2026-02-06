FROM amazoncorretto:21.0.2

ARG ARTIFACT

ENV TZ=America/Montevideo

ENV PROFILE local
ENV SPRINGBOOT_OPTS="-XX:+DoEscapeAnalysis \
-XX:+UseG1GC \
-XX:+ExplicitGCInvokesConcurrent \
-XX:MaxGCPauseMillis=700 \
-verbose:gc \
-Xloggc:/app/logs/gc_$(hostname).log \
-XX:+PrintGCDetails \
-XX:+PrintGCApplicationStoppedTime \
-XX:+UseCompressedOops \
-XX:+UseCompressedClassPointers"

ENV JAVA_OPTS="-Xmx256M -Xms256M -XXMaxRAM=256M \
-XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M"

COPY ${ARTIFACT} /app/backend-app.jar
COPY docker/backend/truststore.jks /app/truststore.jks

WORKDIR /app

EXPOSE 8081/tcp 8180/tcp
