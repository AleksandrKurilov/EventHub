FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build-env
WORKDIR /app

COPY EventHub.HttpApi.Client/*.csproj ./EventHub.HttpApi.Client/
COPY EventHub.Library/*.csproj ./EventHub.Library/
COPY EventHub.Differentlibrary/*.csproj ./EventHub.Differentlibrary/

RUN dotnet restore ./EventHub.HttpApi.Client/EventHub.HttpApi.Client.csproj --no-cache
RUN dotnet restore ./EventHub.Library/EventHub.Library.csproj --no-cache
RUN dotnet restore ./EventHub.Differentlibrary/EventHub.Differentlibrary.csproj --no-cache

COPY EventHub.HttpApi.Client/. ./EventHub.HttpApi.Client/
COPY EventHub.Library/. ./EventHub.Library/
COPY EventHub.Differentlibrary/. ./EventHub.Differentlibrary/

WORKDIR /app/EventHub.HttpApi.Client
RUN dotnet publish EventHub.HttpApi.Client.csproj -c release -o /app/out/ --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /app/out
COPY --from=build-env /app/out ./

ENTRYPOINT ["dotnet", "EventHub.HttpApi.Client.dll"]