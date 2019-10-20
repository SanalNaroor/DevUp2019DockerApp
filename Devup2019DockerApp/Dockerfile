FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Devup2019DockerApp/Devup2019DockerApp.csproj", "Devup2019DockerApp/"]
RUN dotnet restore "Devup2019DockerApp/Devup2019DockerApp.csproj"
COPY . .
WORKDIR "/src/Devup2019DockerApp"
RUN dotnet build "Devup2019DockerApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Devup2019DockerApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Devup2019DockerApp.dll"]