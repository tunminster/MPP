FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 53595
EXPOSE 44350

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY MPP.Web/MPP.Web.csproj MPP.Web/
RUN dotnet restore MPP.Web/MPP.Web.csproj
COPY . .
WORKDIR /src/MPP.Web
RUN dotnet build MPP.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MPP.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MPP.Web.dll"]
