FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY WebApplication1/*.csproj ./WebApplication1/
COPY WebApplication1/*.config ./WebApplication1/
RUN nuget restore

# copy everything else and build app
COPY WebApplication1/. ./WebApplication1/
WORKDIR /app/WebApplication1
RUN msbuild /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/WebApplication1/. ./
