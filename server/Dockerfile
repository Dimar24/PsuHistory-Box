FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["server/PsuHistory-Back/PsuHistory/PsuHistory.csproj", "PsuHistory/"]
COPY ["server/PsuHistory-Back/PsuHistory.Data.Service/PsuHistory.Data.Service.csproj", "PsuHistory.Data.Service/"]
COPY ["server/PsuHistory-Back/PsuHistory.Data.EF.SQL/PsuHistory.Data.EF.SQL.csproj", "PsuHistory.Data.EF.SQL/"]
COPY ["server/PsuHistory-Back/PsuHistory.Data.Domain/PsuHistory.Data.Domain.csproj", "PsuHistory.Data.Domain/"]
COPY ["server/PsuHistory-Back/PsuHistory.Business.Service/PsuHistory.Business.Service.csproj", "PsuHistory.Business.Service/"]
COPY ["server/PsuHistory-Back/PsuHistory.Business.Validation/PsuHistory.Business.Validation.csproj", "PsuHistory.Business.Validation/"]
RUN dotnet restore "PsuHistory/PsuHistory.csproj"
COPY ["server/PsuHistory-Back/", "."]
WORKDIR "/src/PsuHistory"
RUN dotnet build "PsuHistory.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PsuHistory.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PsuHistory.dll"]