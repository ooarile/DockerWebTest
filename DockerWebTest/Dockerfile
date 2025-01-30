# Use the official ASP.NET Core runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app  # 작업 디렉토리를 /app으로 설정합니다.
EXPOSE 80
# 컨테이너의 80번 포트를 외부에 노출합니다.

# Use the .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src  # 소스 코드를 위한 작업 디렉토리를 설정합니다.
COPY ["DockerWebTest/DockerWebTest.csproj", "DockerWebTest/"]  # 프로젝트 파일을 복사합니다.
RUN dotnet restore "DockerWebTest/DockerWebTest.csproj"  # 프로젝트의 종속성을 복원합니다.
COPY . .  # 모든 소스 코드를 컨테이너로 복사합니다.
WORKDIR "/src/DockerWebTest"  # 프로젝트 디렉토리로 이동합니다.
RUN dotnet build "DockerWebTest.csproj" -c Release -o /app/build  # 프로젝트를 Release 모드로 빌드합니다.

# Publish the app
FROM build AS publish
RUN dotnet publish "DockerWebTest.csproj" -c Release -o /app/publish  # 프로젝트를 게시합니다.

# Use the base image to run the app
FROM base AS final
WORKDIR /app  # 작업 디렉토리를 /app으로 설정합니다.
COPY --from=publish /app/publish .  # 게시된 파일을 복사합니다.
ENTRYPOINT ["dotnet", "DockerWebTest.dll"]  # 애플리케이션을 실행합니다.