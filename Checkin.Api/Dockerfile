FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 11620
EXPOSE 44300

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Checkin.Api/Checkin.Api.csproj", "Checkin.Api/"]
RUN dotnet restore "Checkin.Api/Checkin.Api.csproj"
COPY . .
WORKDIR "/src/Checkin.Api"
RUN dotnet build "Checkin.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Checkin.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Checkin.Api.dll"]