#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Holiday.Route.Planner.Web/Holiday.Route.Planner.Web.csproj", "Holiday.Route.Planner.Web/"]
RUN dotnet restore "Holiday.Route.Planner.Web/Holiday.Route.Planner.Web.csproj"
COPY . .
WORKDIR "/src/Holiday.Route.Planner.Web"
RUN dotnet build "Holiday.Route.Planner.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Holiday.Route.Planner.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Holiday.Route.Planner.Web.dll"]
