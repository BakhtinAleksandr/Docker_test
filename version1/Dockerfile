#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["version1/version1.csproj", "version1/"]
RUN dotnet restore "version1/version1.csproj"
COPY . .
WORKDIR "/src/version1"
RUN dotnet build "version1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "version1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "version1.dll"]