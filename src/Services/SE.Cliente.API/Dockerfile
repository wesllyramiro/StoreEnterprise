FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Services/SE.Cliente.API/SE.Cliente.API.csproj", "src/Services/SE.Cliente.API/"]
RUN dotnet restore "src/Services/SE.Cliente.API/SE.Cliente.API.csproj"
COPY . .
WORKDIR "/src/src/Services/SE.Cliente.API"
RUN dotnet build "SE.Cliente.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SE.Cliente.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SE.Cliente.API.dll"]