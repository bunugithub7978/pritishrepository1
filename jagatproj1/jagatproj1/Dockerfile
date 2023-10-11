#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["jagatproj1/jagatproj1.csproj", "jagatproj1/"]
RUN dotnet restore "jagatproj1/jagatproj1.csproj"
COPY . .
WORKDIR "/src/jagatproj1"
RUN dotnet build "jagatproj1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "jagatproj1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "jagatproj1.dll"]