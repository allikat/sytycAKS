FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["thedotnetcorewebapi/thedotnetcorewebapi.csproj", "thedotnetcorewebapi/"]

RUN dotnet restore "thedotnetcorewebapi/thedotnetcorewebapi.csproj"
COPY . .
WORKDIR "/src/thedotnetcorewebapi"
RUN dotnet build "thedotnetcorewebapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "thedotnetcorewebapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "thedotnetcorewebapi.dll"]