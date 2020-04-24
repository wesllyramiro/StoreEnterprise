FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Services/SE.Identidade.API/SE.Identidade.API.csproj", "src/Services/SE.Identidade.API/"]
RUN dotnet restore "src/Services/SE.Identidade.API/SE.Identidade.API.csproj"
COPY . .
WORKDIR "/src/src/Services/SE.Identidade.API"
RUN dotnet build "SE.Identidade.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SE.Identidade.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SE.Identidade.API.dll"]