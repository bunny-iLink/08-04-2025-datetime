# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy solution and project files
COPY csharp-backend/backend.csproj ./csharp-backend/
COPY csharp-backend/timeapi.sln ./

# Restore dependencies
RUN dotnet restore ./timeapi.sln

# Copy everything else
COPY csharp-backend/ ./csharp-backend/

# Publish the application
RUN dotnet publish ./csharp-backend/backend.csproj -c Release -o /out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /out .

ENTRYPOINT ["dotnet", "backend.dll"]
