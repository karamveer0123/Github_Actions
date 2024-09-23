FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5007
COPY Dockerfile /root

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["technosavvy.mAPI.csproj", "Technosavvy.mAPI/"]
RUN dotnet restore "Technosavvy.mAPI/technosavvy.mAPI.csproj"
COPY . .
WORKDIR /src
RUN dotnet build "technosavvy.mAPI.csproj" -c Release -o /app/build /p:UseAppHost=false

FROM build AS publish
RUN dotnet publish "technosavvy.mAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
RUN apt-get update && apt-get install curl -y
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "technosavvy.mAPI.dll"]
