FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
# set up network
ENV ASPNETCORE_URLS http://+:8080
EXPOSE 8080

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY /Web1.csproj Web1/
RUN dotnet restore Web1/Web1.csproj
COPY . .
WORKDIR /src/Web1
RUN dotnet build Web1.csproj -c Release -o /out

FROM build AS publish
RUN dotnet publish Web1.csproj -c Release -o /out

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web1.dll", "--server.urls", "http://0.0.0.0:8080"]



#FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
#WORKDIR /src
#COPY Web1/Web1.csproj Web1/
#RUN dotnet restore Web1/Web1.csproj
#COPY . .
#WORKDIR /src/Web1
#RUN dotnet build Web1.csproj -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish Web1.csproj -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "Web1.dll"]
#

#FROM microsoft/aspnetcore-build:2.0 AS build
#WORKDIR /build
#COPY . .
#RUN dotnet restore
#RUN dotnet publish -c Release -o output
#
#
#FROM microsoft/aspnetcore:2.0
#WORKDIR /app
#COPY --from=build /build/output .
#ENTRYPOINT ["dotnet", "Web1.dll"]
#
