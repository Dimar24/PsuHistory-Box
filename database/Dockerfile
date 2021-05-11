FROM mcr.microsoft.com/mssql/server AS base

ENV ACCEPT_EULA=Y
ENV SA_PASSWORD=Pa55w0rd2021

COPY . .
COPY ["Db/Scripts/*", "Db/Scripts/"]
VOLUME ./Db:/var/opt/mssql/data

HEALTHCHECK --interval=10s --timeout=5s --start-period=10s --retries=10 \
    CMD /opt/mssql-tools/bin/sqlcmd -S . -U sa -P Password123 -i Db/Scripts/SetupDb.sql || exit 1