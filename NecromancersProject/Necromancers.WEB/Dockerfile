FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Necromancers.WEB/Necromancers.WEB.csproj", "Necromancers.WEB/"]
RUN dotnet restore "Necromancers.WEB/Necromancers.WEB.csproj"
COPY . .
WORKDIR "/src/Necromancers.WEB"
RUN dotnet build "Necromancers.WEB.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Necromancers.WEB.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Necromancers.WEB.dll"]
