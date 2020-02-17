#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Ms_Cotizacion/Ms_Cotizacion.fsproj", "Ms_Cotizacion/"]
RUN dotnet restore "Ms_Cotizacion/Ms_Cotizacion.fsproj"
COPY . .
WORKDIR "/src/Ms_Cotizacion"
RUN dotnet build "Ms_Cotizacion.fsproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Ms_Cotizacion.fsproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Ms_Cotizacion.dll"]