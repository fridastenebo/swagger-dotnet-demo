FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Fribb.SwaggerDotnetDemo/Fribb.SwaggerDotnetDemo.csproj", "Fribb.SwaggerDotnetDemo/"]
RUN dotnet restore "Fribb.SwaggerDotnetDemo/Fribb.SwaggerDotnetDemo.csproj"
COPY . .
WORKDIR "/src/Fribb.SwaggerDotnetDemo"
RUN dotnet build "Fribb.SwaggerDotnetDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Fribb.SwaggerDotnetDemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Fribb.SwaggerDotnetDemo.dll"]
