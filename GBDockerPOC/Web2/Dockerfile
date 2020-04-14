FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
# set up network
ENV ASPNETCORE_URLS http://+:8081
EXPOSE 8081

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Web2/Web2.csproj Web2/
RUN dotnet restore Web2/Web2.csproj
COPY . .
WORKDIR /src/Web2
RUN dotnet build Web2.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Web2.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web2.dll", "--server.urls", "http://0.0.0.0:8081"]




#FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base
#WORKDIR /app
#EXPOSE 81
#
#FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
#WORKDIR /src
#COPY Web2/Web2.csproj Web2/
#RUN dotnet restore Web2/Web2.csproj
#COPY . .
#WORKDIR /src/Web2
#RUN dotnet build Web2.csproj -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish Web2.csproj -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "Web2.dll"]
#
#
#FROM microsoft/aspnetcore-build:2.0 AS build2
#WORKDIR /build2
#COPY . .
#RUN dotnet restore
#RUN dotnet publish -c Release -o output
#
#
#FROM microsoft/aspnetcore:2.0
#WORKDIR /app2
#COPY --from=build2 /build2/output .
#ENTRYPOINT ["dotnet", "Web2.dll"]
#