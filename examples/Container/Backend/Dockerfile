FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build-env
WORKDIR /app

# Copy everything
COPY . ./
RUN dotnet --info
RUN dotnet restore examples/Container/Backend
RUN dotnet publish examples/Container/Backend -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Backend.dll"]