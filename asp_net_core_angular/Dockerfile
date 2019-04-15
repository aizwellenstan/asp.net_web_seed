FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["asp_net_core_angular/asp_net_core_angular.csproj", "asp_net_core_angular/"]
RUN dotnet restore "asp_net_core_angular/asp_net_core_angular.csproj"
COPY . .
WORKDIR "/src/asp_net_core_angular"
RUN dotnet build "asp_net_core_angular.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "asp_net_core_angular.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "asp_net_core_angular.dll"]