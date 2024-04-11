
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Devops_demo_project/Devops_demo_project.csproj", "Devops_demo_project/"]
RUN dotnet restore "Devops_demo_project/Devops_demo_project.csproj"
COPY . .
WORKDIR "/src/Devops_demo_project"
RUN dotnet build "Devops_demo_project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Devops_demo_project.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Devops_demo_project.dll"]