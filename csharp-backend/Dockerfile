# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy only what is necessary for restore
COPY csharp-backend/timeapi.sln ./
COPY csharp-backend/backend.csproj ./

# Restore
RUN dotnet restore timeapi.sln

# Copy the rest of the backend project
COPY csharp-backend/. .

# Build and publish the app
RUN dotnet publish backend.csproj -c Release -o /out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /out .

ENTRYPOINT ["dotnet", "backend.dll"]
