#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SimpleApiWithHttpsAndDocker/SimpleApiWithHttpsAndDocker.csproj", "SimpleApiWithHttpsAndDocker/"]
RUN dotnet restore "SimpleApiWithHttpsAndDocker/SimpleApiWithHttpsAndDocker.csproj"
COPY . .
WORKDIR "/src/SimpleApiWithHttpsAndDocker"
RUN dotnet build "SimpleApiWithHttpsAndDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleApiWithHttpsAndDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleApiWithHttpsAndDocker.dll"]


#run from  C:\Code\Core\SimpleApiWithHttpsAndDocker> docker build -t marcus/simpleapiwithhttpsanddocker -f simpleapiwithhttpsanddocker/Dockerfile .