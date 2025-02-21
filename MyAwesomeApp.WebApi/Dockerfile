FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MyAwesomeApp.WebApi/MyAwesomeApp.WebApi.csproj", "MyAwesomeApp.WebApi/"]
RUN dotnet restore "MyAwesomeApp.WebApi/MyAwesomeApp.WebApi.csproj"
COPY . .
WORKDIR "/src/MyAwesomeApp.WebApi"
RUN dotnet build "MyAwesomeApp.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyAwesomeApp.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyAwesomeApp.WebApi.dll"]