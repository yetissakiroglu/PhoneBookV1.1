#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Services/Report/Phonebook.Services.Report/Phonebook.Services.Report.csproj", "Services/Report/Phonebook.Services.Report/"]
COPY ["Shared/Phonebook.Shared/Phonebook.Shared.csproj", "Shared/Phonebook.Shared/"]
RUN dotnet restore "Services/Report/Phonebook.Services.Report/Phonebook.Services.Report.csproj"
COPY . .
WORKDIR "/src/Services/Report/Phonebook.Services.Report"
RUN dotnet build "Phonebook.Services.Report.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Phonebook.Services.Report.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Phonebook.Services.Report.dll"]