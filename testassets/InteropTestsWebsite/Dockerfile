FROM mcr.microsoft.com/dotnet/nightly/sdk:9.0-preview AS build-env
WORKDIR /app

# Copy everything
COPY . ./
RUN dotnet --info
RUN dotnet restore testassets/InteropTestsWebsite
RUN dotnet publish testassets/InteropTestsWebsite --framework net9.0 -c Release -o out -p:LatestFramework=true

# Build runtime image
FROM mcr.microsoft.com/dotnet/nightly/aspnet:9.0-preview
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "InteropTestsWebsite.dll", "--port_http1", "80"]