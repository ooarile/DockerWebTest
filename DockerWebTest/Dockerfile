# Use the .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src  # 소스 코드를 위한 작업 디렉토리를 설정합니다.
COPY ["DockerWebTest.csproj", "./"]
RUN dotnet restore  # 프로젝트의 종속성을 복원합니다.
COPY . .
RUN dotnet publish -c Release -o /app/publish  # 프로젝트를 Release 모드로 게시합니다.

# Use the official ASP.NET Core runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app  # 작업 디렉토리를 /app으로 설정합니다.
EXPOSE 80  
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "DockerWebTest.dll"]  # 애플리케이션을 실행합니다.