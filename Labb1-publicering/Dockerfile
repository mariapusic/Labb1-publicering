#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Labb1-publicering.csproj", "."]
RUN dotnet restore "Labb1-publicering/Labb1-publicering.csproj"
COPY . .
RUN dotnet build "Labb1-publicering.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Labb1-publicering.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Labb1-publicering.dll"]