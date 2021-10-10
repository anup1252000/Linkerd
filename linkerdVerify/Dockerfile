FROM mcr.microsoft.com/dotnet/aspnet:3.1-focal AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443


FROM mcr.microsoft.com/dotnet/sdk:3.1-focal AS build
WORKDIR /src
COPY ["linkerdVerify.csproj", "./"]
RUN dotnet restore "linkerdVerify.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "linkerdVerify.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "linkerdVerify.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "linkerdVerify.dll"]
