FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["MicroShopping/MicroShopping.csproj", "MicroShopping/"]
RUN dotnet restore "MicroShopping/MicroShopping.csproj"
COPY . .
WORKDIR "/src/MicroShopping"
RUN dotnet build "MicroShopping.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroShopping.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroShopping.dll"]