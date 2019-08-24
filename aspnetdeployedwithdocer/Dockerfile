#FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
#WORKDIR /src
#COPY ["aspnetdeployedwithdocer/aspnetdeployedwithdocer.csproj", "aspnetdeployedwithdocer/"]
#RUN dotnet restore "aspnetdeployedwithdocer/aspnetdeployedwithdocer.csproj"
#COPY . .
#WORKDIR "/src/aspnetdeployedwithdocer"
#RUN dotnet build "aspnetdeployedwithdocer.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "aspnetdeployedwithdocer.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "aspnetdeployedwithdocer.dll"]

FROM microsoft/dotnet:sdk AS build-env

WORKDIR /app

# Copy csproj and restore as distinct layers

COPY *.csproj ./

RUN dotnet restore

# Copy everything else and build

COPY . ./

RUN dotnet publish -c Release -o out

# Build runtime image

FROM microsoft/dotnet:aspnetcore-runtime

WORKDIR /app

COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "aspnetdeployedwithdocer.dll"]