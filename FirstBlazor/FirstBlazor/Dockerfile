#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["FirstBlazor/FirstBlazor.csproj", "FirstBlazor/"]
RUN dotnet restore "FirstBlazor/FirstBlazor.csproj"
COPY . .
WORKDIR "/src/FirstBlazor"
RUN dotnet build "FirstBlazor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FirstBlazor.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FirstBlazor.dll"]