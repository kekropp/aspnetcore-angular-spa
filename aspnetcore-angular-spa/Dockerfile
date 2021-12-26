#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["aspnetcore-angular-spa/aspnetcore-angular-spa.csproj", "Apollo/"]
RUN dotnet restore "aspnetcore-angular-spa/aspnetcore-angular-spa.csproj"
COPY . .
WORKDIR "/src/aspnetcore-angular-spa"
RUN dotnet build "aspnetcore-angular-spa.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore-angular-spa.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore-angular-spa.dll"]