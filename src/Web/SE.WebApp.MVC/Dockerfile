FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Web/SE.WebApp.MVC/SE.WebApp.MVC.csproj", "src/Web/SE.WebApp.MVC/"]
RUN dotnet restore "src/Web/SE.WebApp.MVC/SE.WebApp.MVC.csproj"
COPY . .
WORKDIR "/src/src/Web/SE.WebApp.MVC"
RUN dotnet build "SE.WebApp.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SE.WebApp.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SE.WebApp.MVC.dll"]