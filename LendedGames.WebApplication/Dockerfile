#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["LendedGames.WebApplication/LendedGames.WebApplication.csproj", "LendedGames.WebApplication/"]
RUN dotnet restore "LendedGames.WebApplication/LendedGames.WebApplication.csproj"
COPY . .
WORKDIR "/src/LendedGames.WebApplication"
RUN dotnet build "LendedGames.WebApplication.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LendedGames.WebApplication.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LendedGames.WebApplication.dll"]