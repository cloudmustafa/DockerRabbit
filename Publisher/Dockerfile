FROM microsoft/dotnet:2.2-sdk AS build

ARG BUILDCONFIG=RELEASE
ARG VERSION=1.0.0

COPY Publisher.csproj /build/
RUN dotnet restore ./build/Publisher.csproj

# Copy everything else and build
COPY . ./build/

WORKDIR /build/
RUN dotnet publish ./Publisher.csproj -c ${BUILDCONFIG} -o out /p:Version=${VERSION}

# Build runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime AS runtime

WORKDIR /app

COPY --from=build /build/out .

ENTRYPOINT ["dotnet", "Publisher.dll"]