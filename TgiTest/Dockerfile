#FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
#WORKDIR /src
#COPY ["./TgiTest.csproj", "TgiTest/"]
#RUN dotnet restore "TgiTest/TgiTest.csproj"
#COPY . .
#WORKDIR "/src/TgiTest"
#RUN dotnet build "TgiTest.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "TgiTest.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "TgiTest.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["./TgiTest.csproj", "TgiTest/"]
RUN dotnet restore "TgiTest/TgiTest.csproj"
COPY . .
WORKDIR "/src/TgiTest"
# Replaced dotnet build with dotnet publish for web API project
RUN dotnet build "TgiTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TgiTest.csproj" -c Release -o /app/publish
# This stage is no longer needed since publish happens in build stage
# RUN dotnet publish "TgiTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TgiTest.dll"]

