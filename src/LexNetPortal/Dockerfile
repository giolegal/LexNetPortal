FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["LexNetPortal/LexNetPortal.csproj", "LexNetPortal/"]
RUN dotnet restore "LexNetPortal/LexNetPortal.csproj"
COPY . .
WORKDIR "/src/LexNetPortal"
RUN dotnet build "LexNetPortal.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LexNetPortal.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LexNetPortal.dll"]