FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["miwebapp1/miwebapp1.csproj", "miwebapp1/"]
RUN dotnet restore "miwebapp1/miwebapp1.csproj"
COPY . .
WORKDIR "/src/miwebapp1"
RUN dotnet build "miwebapp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "miwebapp1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "miwebapp1.dll"]
