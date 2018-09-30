FROM microsoft/dotnet:2.1-sdk-alpine AS pub
WORKDIR /app/
COPY *.csproj ./
RUN dotnet restore

COPY ./ ./
WORKDIR /app/
RUN dotnet publish -c Release -o pub

# test layer
# # test application -- see: dotnet-docker-unit-testing.md
# #FROM build AS testrunner
# #WORKDIR /app/tests
# #COPY tests/. .
# #ENTRYPOINT ["dotnet", "test", "--logger:trx"]

FROM microsoft/dotnet:2.1-runtime-alpine AS runtime

ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT false
RUN apk add --no-cache icu-libs

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

WORKDIR /app/
COPY --from=pub /app/pub/ ./
ENTRYPOINT ["dotnet", "console.dll"]