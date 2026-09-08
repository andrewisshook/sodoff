# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy the source code
COPY . .

# Restore dependencies first
RUN dotnet restore

# Build and publish the application
RUN dotnet publish -c Release -o /app

# Move mods and assets directories from sources to /app
RUN mv src/mods /app && ln -s /app/mods src/
RUN mv src/assets /app && ln -s /app/assets src/

# Create clean run environment (without source and sdk)
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app

COPY --from=build /app .

# Run the application
ENTRYPOINT ["./sodoff"]
