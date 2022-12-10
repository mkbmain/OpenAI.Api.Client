FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["OpenAI.Api.Client/OpenAI.Api.Client.csproj", "OpenAI.Api.Client/"]
RUN dotnet restore "OpenAI.Api.Client/OpenAI.Api.Client.csproj"
COPY . .
WORKDIR "/src/OpenAI.Api.Client"
RUN dotnet build "OpenAI.Api.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OpenAI.Api.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OpenAI.Api.Client.dll"]
