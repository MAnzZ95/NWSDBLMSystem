#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["NWSDBLMSystem.Configuration.Web.Api/NWSDBLMSystem.Configuration.Web.Api.csproj", "NWSDBLMSystem.Configuration.Web.Api/"]
RUN dotnet restore "NWSDBLMSystem.Configuration.Web.Api/NWSDBLMSystem.Configuration.Web.Api.csproj"
COPY . .
WORKDIR "/src/NWSDBLMSystem.Configuration.Web.Api"
RUN dotnet build "NWSDBLMSystem.Configuration.Web.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NWSDBLMSystem.Configuration.Web.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NWSDBLMSystem.Configuration.Web.Api.dll"]