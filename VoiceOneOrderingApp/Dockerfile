#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["VoiceOneOrderingApp.csproj", "voiceoneorderapp/"]
RUN dotnet restore "voiceoneorderapp/VoiceOneOrderingApp.csproj"
COPY . ./



FROM build AS publish
RUN dotnet publish "VoiceOneOrderingApp.csproj" -c Release -o /app/publish

WORKDIR "/src/voiceoneorderapp"

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VoiceOneOrderingApp.dll"]