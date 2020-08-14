FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["services/MasterCoder.API/MasterCoder.API.csproj", "services/MasterCoder.API/"]
RUN dotnet restore "services/MasterCoder.API/MasterCoder.API.csproj"
COPY . .
WORKDIR "/src/services/MasterCoder.API"
RUN dotnet build "MasterCoder.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MasterCoder.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MasterCoder.API.dll"]