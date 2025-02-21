FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MyAwesomeApp.CronJob/MyAwesomeApp.CronJob.csproj", "MyAwesomeApp.CronJob/"]
RUN dotnet restore "MyAwesomeApp.CronJob/MyAwesomeApp.CronJob.csproj"
COPY . .
WORKDIR "/src/MyAwesomeApp.CronJob"
RUN dotnet publish "MyAwesomeApp.CronJob.csproj" -c Release -o /app/publish

FROM build AS publish

FROM mcr.microsoft.com/dotnet/runtime:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyAwesomeApp.CronJob.dll"]