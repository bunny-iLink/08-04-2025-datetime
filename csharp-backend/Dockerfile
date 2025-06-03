# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy solution and project files
COPY timeapi.sln .
COPY backend.csproj .

# Restore dependencies
RUN dotnet restore timeapi.sln

# Copy everything else
COPY . ./

# Publish the application
RUN dotnet publish backend.csproj -c Release -o /out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /out .

# Set the entry point
ENTRYPOINT ["dotnet", "backend.dll"]
