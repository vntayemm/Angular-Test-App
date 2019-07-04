FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY EBTestApplication/*.csproj ./EBTestApplication/
COPY EBTestApplication/*.config ./EBTestApplication/
RUN nuget restore

# copy everything else and build app
COPY EBTestApplication/. ./EBTestApplication/
WORKDIR /app/EBTestApplication
RUN msbuild /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/EBTestApplication/. ./
