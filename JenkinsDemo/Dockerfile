#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["JenkinsDemo/JenkinsDemo.csproj", "/JenkinsDemo"]
RUN dotnet restore "JenkinsDemo/JenkinsDemo.csproj"
COPY . .
WORKDIR "/src/JenkinsDemo"
RUN dotnet build "JenkinsDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JenkinsDemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsDemo.dll"]
#
#FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
#WORKDIR /app
#
#COPY *_csproj .
#
#RUN dotnet restore  
#
#COPY . ./
#
#RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false
#
#FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "JenkinsDemo.dll"]