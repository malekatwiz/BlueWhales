FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 2765
EXPOSE 44335

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY BlueWhales.Security/BlueWhales.Security.csproj BlueWhales.Security/
RUN dotnet restore BlueWhales.Security/BlueWhales.Security.csproj
COPY . .
WORKDIR /src/BlueWhales.Security
RUN dotnet build BlueWhales.Security.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish BlueWhales.Security.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BlueWhales.Security.dll"]
