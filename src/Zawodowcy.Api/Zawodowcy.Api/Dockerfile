FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Zawodowcy.Api/Zawodowcy.Api.csproj", "Zawodowcy.Api/"]
RUN dotnet restore "Zawodowcy.Api/Zawodowcy.Api.csproj"
COPY . .
WORKDIR "/src/Zawodowcy.Api"
RUN dotnet build "Zawodowcy.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Zawodowcy.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["dotnet", "Zawodowcy.Api.dll"]
