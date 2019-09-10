FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["corewebapp/corewebapp.csproj", "corewebapp/"]
RUN dotnet restore "corewebapp/corewebapp.csproj"
COPY . .
WORKDIR "/src/corewebapp"
RUN dotnet build "corewebapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "corewebapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "corewebapp.dll"]