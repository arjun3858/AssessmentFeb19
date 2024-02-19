#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["AssessmentFeb19/AssessmentFeb19.csproj", "AssessmentFeb19/"]
RUN dotnet restore "./AssessmentFeb19/./AssessmentFeb19.csproj"
COPY . .
WORKDIR "/src/AssessmentFeb19"
RUN dotnet build "./AssessmentFeb19.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./AssessmentFeb19.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AssessmentFeb19.dll"]