FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ContainerWebApp/ContainerWebApp.csproj", "ContainerWebApp/"]
RUN dotnet restore "ContainerWebApp/ContainerWebApp.csproj"
COPY . .
WORKDIR "/src/ContainerWebApp"
RUN dotnet build "ContainerWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ContainerWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ContainerWebApp.dll"]