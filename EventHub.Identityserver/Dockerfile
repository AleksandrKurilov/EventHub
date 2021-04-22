FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build-env
WORKDIR /app

COPY EventHub.Identityserver/*.csproj ./EventHub.Identityserver/
COPY EventHub.Library/*.csproj ./EventHub.Library/
COPY EventHub.Differentlibrary/*.csproj ./EventHub.Differentlibrary/

RUN dotnet restore ./EventHub.Identityserver/EventHub.Identityserver.csproj --no-cache
RUN dotnet restore ./EventHub.Library/EventHub.Library.csproj --no-cache
RUN dotnet restore ./EventHub.Differentlibrary/EventHub.Differentlibrary.csproj --no-cache

COPY EventHub.Identityserver/. ./EventHub.Identityserver/
COPY EventHub.Library/. ./EventHub.Library/
COPY EventHub.Differentlibrary/. ./EventHub.Differentlibrary/

WORKDIR /app/EventHub.Identityserver
RUN dotnet publish EventHub.Identityserver.csproj -c release -o /app/out/ --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /app/out
COPY --from=build-env /app/out ./

ENTRYPOINT ["dotnet", "EventHub.Identityserver.dll"]