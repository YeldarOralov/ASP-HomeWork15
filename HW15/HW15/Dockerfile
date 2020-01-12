FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["HW15/HW15.csproj", "HW15/"]
RUN dotnet restore "HW15/HW15.csproj"
COPY . .
WORKDIR "/src/HW15"
RUN dotnet build "HW15.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HW15.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HW15.dll"]