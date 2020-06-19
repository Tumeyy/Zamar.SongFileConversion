FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Zamzar.SongFileConversion/Zamzar.SongFileConversion.csproj", "Zamzar.SongFileConversion/"]
RUN dotnet restore "Zamzar.SongFileConversion/Zamzar.SongFileConversion.csproj"
COPY . .
WORKDIR "/src/Zamzar.SongFileConversion"
RUN dotnet build "Zamzar.SongFileConversion.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Zamzar.SongFileConversion.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Zamzar.SongFileConversion.dll"]