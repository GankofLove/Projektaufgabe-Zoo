FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Projektaufgabe-Zoo/Projektaufgabe-Zoo.csproj", "Projektaufgabe-Zoo/"]
RUN dotnet restore "Projektaufgabe-Zoo/Projektaufgabe-Zoo.csproj"
COPY . .
WORKDIR "/src/Projektaufgabe-Zoo"
RUN dotnet build "Projektaufgabe-Zoo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Projektaufgabe-Zoo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Projektaufgabe-Zoo.dll"]
