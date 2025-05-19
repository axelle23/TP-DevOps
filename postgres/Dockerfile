FROM postgres:17.2-alpine

ENV POSTGRES_DB=db \
   POSTGRES_USER=abrosse

COPY CreateScheme.sql InsertData.sql /docker-entrypoint-initdb.d/
