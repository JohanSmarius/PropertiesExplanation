FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["PropertiesExplanation/PropertiesExplanation.csproj", "PropertiesExplanation/"]
RUN dotnet restore "PropertiesExplanation/PropertiesExplanation.csproj"
COPY . .
WORKDIR "/src/PropertiesExplanation"
RUN dotnet build "PropertiesExplanation.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PropertiesExplanation.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PropertiesExplanation.dll"]
