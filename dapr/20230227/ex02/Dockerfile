FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ex02.csproj", "."]
RUN dotnet restore "./ex02.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "ex02.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ex02.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ex02.dll"]