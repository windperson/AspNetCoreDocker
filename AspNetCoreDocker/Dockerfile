FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AspNetCoreDocker/AspNetCoreDocker.csproj", "AspNetCoreDocker/"]
RUN dotnet restore "AspNetCoreDocker/AspNetCoreDocker.csproj"
COPY . .
WORKDIR "/src/AspNetCoreDocker"
RUN dotnet build "AspNetCoreDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetCoreDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreDocker.dll"]
