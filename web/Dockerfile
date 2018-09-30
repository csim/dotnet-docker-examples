FROM microsoft/dotnet:2.1-sdk-alpine AS pub

WORKDIR /app/
COPY *.csproj ./
RUN dotnet restore

COPY ./ ./
WORKDIR /app/
RUN dotnet publish -c Release -o pub

FROM microsoft/dotnet:2.1-aspnetcore-runtime-alpine AS runtime

WORKDIR /app/
COPY --from=pub /app/pub/ ./
ENTRYPOINT ["dotnet", "web.dll"]