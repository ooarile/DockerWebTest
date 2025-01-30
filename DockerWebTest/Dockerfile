FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["DockerWebTest.csproj", "."]
RUN dotnet restore "./DockerWebTest.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet publish "DockerWebTest.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "DockerWebTest.dll"]