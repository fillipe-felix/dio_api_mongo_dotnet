FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["dio_api_mongo_dotnet/dio_api_mongo_dotnet.csproj", "dio_api_mongo_dotnet/"]
RUN dotnet restore "dio_api_mongo_dotnet/dio_api_mongo_dotnet.csproj"
COPY . .
WORKDIR "/src/dio_api_mongo_dotnet"
RUN dotnet build "dio_api_mongo_dotnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dio_api_mongo_dotnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dio_api_mongo_dotnet.dll"]
