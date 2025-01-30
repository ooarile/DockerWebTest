FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["DockerWebTest/DockerWebTest.csproj", "DockerWebTest/"]
RUN dotnet restore "DockerWebTest/DockerWebTest.csproj"
COPY . .
WORKDIR "/src/DockerWebTest"
RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "DockerWebTest.dll"]