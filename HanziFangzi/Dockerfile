FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["HanziFangzi/HanziFangzi.csproj", "HanziFangzi/"]
RUN dotnet restore "HanziFangzi/HanziFangzi.csproj"
COPY . .
WORKDIR "/src/HanziFangzi"
RUN dotnet build "HanziFangzi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HanziFangzi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HanziFangzi.dll"]
