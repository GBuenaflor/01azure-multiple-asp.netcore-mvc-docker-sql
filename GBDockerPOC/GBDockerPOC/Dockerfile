FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
WORKDIR /src
COPY GBDockerPOC/GBDockerPOC.csproj GBDockerPOC/
RUN dotnet restore GBDockerPOC/GBDockerPOC.csproj
COPY . .
WORKDIR /src/GBDockerPOC
RUN dotnet build GBDockerPOC.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish GBDockerPOC.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GBDockerPOC.dll"]
