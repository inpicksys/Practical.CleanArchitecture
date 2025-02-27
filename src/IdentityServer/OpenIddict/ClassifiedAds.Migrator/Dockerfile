FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build-env
WORKDIR /ClassifiedAds.Monolith

# Copy csproj and restore as distinct layers
COPY ./ClassifiedAds.Application/*.csproj ./ClassifiedAds.Application/
COPY ./ClassifiedAds.ArchTests/*.csproj ./ClassifiedAds.ArchTests/
COPY ./ClassifiedAds.BackgroundServer/*.csproj ./ClassifiedAds.BackgroundServer/
COPY ./ClassifiedAds.Blazor.Modules/*.csproj ./ClassifiedAds.Blazor.Modules/
COPY ./ClassifiedAds.BlazorServerSide/*.csproj ./ClassifiedAds.BlazorServerSide/
COPY ./ClassifiedAds.BlazorWebAssembly/*.csproj ./ClassifiedAds.BlazorWebAssembly/
COPY ./ClassifiedAds.ContractTests/*.csproj ./ClassifiedAds.ContractTests/
COPY ./ClassifiedAds.CrossCuttingConcerns/*.csproj ./ClassifiedAds.CrossCuttingConcerns/
COPY ./ClassifiedAds.Domain/*.csproj ./ClassifiedAds.Domain/
COPY ./ClassifiedAds.EndToEndTests/*.csproj ./ClassifiedAds.EndToEndTests/
COPY ./ClassifiedAds.GraphQL/*.csproj ./ClassifiedAds.GraphQL/
COPY ./ClassifiedAds.IdentityServer/*.csproj ./ClassifiedAds.IdentityServer/
COPY ./ClassifiedAds.Infrastructure/*.csproj ./ClassifiedAds.Infrastructure/
COPY ./ClassifiedAds.IntegrationTests/*.csproj ./ClassifiedAds.IntegrationTests/
COPY ./ClassifiedAds.Migrator/*.csproj ./ClassifiedAds.Migrator/
COPY ./ClassifiedAds.Persistence/*.csproj ./ClassifiedAds.Persistence/
COPY ./ClassifiedAds.UnitTests/*.csproj ./ClassifiedAds.UnitTests/
COPY ./ClassifiedAds.WebAPI/*.csproj ./ClassifiedAds.WebAPI/
COPY ./ClassifiedAds.WebMVC/*.csproj ./ClassifiedAds.WebMVC/
COPY ./ClassifiedAds.Monolith.sln .
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish ./ClassifiedAds.Migrator/ClassifiedAds.Migrator.csproj -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /ClassifiedAds.Monolith
COPY --from=build-env /ClassifiedAds.Monolith/out .

ENTRYPOINT ["dotnet", "ClassifiedAds.Migrator.dll"]