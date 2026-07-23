FROM eclipse-temurin:17-jre

RUN mkdir -p /app/plugins

# Metabase v0.52.13
ADD https://downloads.metabase.com/v0.52.13/metabase.jar /app/metabase.jar

# DuckDB Driver для MotherDuck / DuckDB
ADD https://github.com/MotherDuck-Open-Source/metabase_duckdb_driver/releases/download/0.2.12-b/duckdb.metabase-driver.jar /app/plugins/

RUN chmod 644 /app/metabase.jar \
    && chmod 644 /app/plugins/duckdb.metabase-driver.jar

ENV MB_PLUGINS_DIR=/app/plugins
ENV JAVA_OPTS="-Xmx2g"

WORKDIR /app

EXPOSE 3000

CMD ["java", "-jar", "/app/metabase.jar"]