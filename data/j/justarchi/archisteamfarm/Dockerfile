FROM microsoft/dotnet:2.1-sdk AS build-env  
ENV NET_CORE_VERSION netcoreapp2.1  
WORKDIR /app  
COPY . ./  
RUN dotnet --info && \  
dotnet publish ArchiSteamFarm -c Release -f "$NET_CORE_VERSION" -o out /nologo
/p:ASFVariant=docker /p:LinkDuringPublish=false && \  
cp "ArchiSteamFarm/scripts/generic/ArchiSteamFarm.sh"
"ArchiSteamFarm/out/ArchiSteamFarm.sh"  
  
FROM microsoft/dotnet:2.1-runtime-stretch-slim-arm32v7  
LABEL maintainer="JustArchi <JustArchi@JustArchi.net>"  
EXPOSE 1242  
WORKDIR /app  
COPY \--from=build-env /app/ArchiSteamFarm/out ./  
ENTRYPOINT ["./ArchiSteamFarm.sh", "--no-restart", "--process-required", "--
system-required"]  

