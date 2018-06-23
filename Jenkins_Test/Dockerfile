FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56231
EXPOSE 44336

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Jenkins_Test/Jenkins_Test.csproj Jenkins_Test/
RUN dotnet restore Jenkins_Test/Jenkins_Test.csproj
COPY . .
WORKDIR /src/Jenkins_Test
RUN dotnet build Jenkins_Test.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Jenkins_Test.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Jenkins_Test.dll"]
