FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ConsoleApp65/ConsoleApp65.csproj", "ConsoleApp65/"]
RUN dotnet restore "ConsoleApp65/ConsoleApp65.csproj"
COPY . .
WORKDIR "/src/ConsoleApp65"
RUN dotnet build "ConsoleApp65.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleApp65.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp65.dll"]
