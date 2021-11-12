FROM adoptopenjdk/openjdk11:alpine-jre as builder

RUN mkdir -p /app

COPY web-app/target/web-app.jar /app/app.jar
WORKDIR /app

RUN java -Djarmode=layertools -jar app.jar extract

FROM adoptopenjdk/openjdk11:alpine-jre

RUN mkdir -p /opt/cprof && \
    wget -q -O- https://storage.googleapis.com/cloud-profiler/java/latest/profiler_java_agent.tar.gz \
    | tar xzv -C /opt/cprof

RUN mkdir -p /app /app/logs \
  && touch /app/logs/gc.log

WORKDIR app
COPY --from=builder app/dependencies/ ./
COPY --from=builder app/spring-boot-loader/ ./
COPY --from=builder app/snapshot-dependencies/ ./
COPY --from=builder app/application/ ./

RUN chmod 777 -R /app \
  && chmod 777 -R /app/logs
  
  
EXPOSE 8080 8081

ARG app_version=""
ENV INFO_APP_VERSION=$app_version

ENV MALLOC_ARENA_MAX=2

ENV JVM_SETTINGS="-XX:MaxMetaspaceSize=256m -XshowSettings:vm -XX:+UseG1GC -XX:MaxDirectMemorySize=64m -XX:NativeMemoryTracking=off"
ENV PROFILER_OPTIONS=""

CMD java \  
  -XX:+HeapDumpOnOutOfMemoryError \
  -XX:HeapDumpPath=/app/logs/ \
   $JVM_SETTINGS \
   ${PROFILER_OPTIONS} \
  -server \
  -Dcom.sun.management.jmxremote  \
  -Dcom.sun.management.jmxremote.authenticate=false \
  -Dcom.sun.management.jmxremote.ssl=false \
  -Dcom.sun.management.jmxremote.local.only=false \
  -Dcom.sun.management.jmxremote.port=1099 \
  -Dcom.sun.management.jmxremote.rmi.port=1099 \
  -Djava.rmi.server.hostname=127.0.0.1 \
  -Duser.timezone=UTC \
  -Djava.security.egd=file:/dev/./urandom \
   org.springframework.boot.loader.JarLauncher