FROM mcr.microsoft.com/dotnet/core/sdk:3.0-alpine as build

WORKDIR /src

COPY Site.csproj .
RUN dotnet restore

COPY . .
RUN dotnet build -c Release

# RUN dotnet test ...

RUN dotnet publish -c Release -o /dist


FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-alpine

WORKDIR /app

ENV ASPNETCORE_ENVIRONMENT Production
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80

COPY --from=build /dist /app
CMD ["dotnet", "Site.dll"]
