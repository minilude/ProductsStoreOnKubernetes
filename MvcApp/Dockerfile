FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 3317
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY ["/MvcApp.csproj", "MvcApp/"]
RUN dotnet restore "MvcApp/MvcApp.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "MvcApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MvcApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MvcApp.dll"]