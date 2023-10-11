#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ITP_Recknagel.API/ITP_Recknagel.API.csproj", "ITP_Recknagel.API/"]
RUN dotnet restore "ITP_Recknagel.API/ITP_Recknagel.API.csproj"
COPY . .
WORKDIR "/src/ITP_Recknagel.API"
RUN dotnet build "ITP_Recknagel.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ITP_Recknagel.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ITP_Recknagel.API.dll"]