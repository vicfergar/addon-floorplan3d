# Use the ASP.NET runtime image to run the application
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

RUN apt-get update && apt-get install -y wget unzip && \
    wget https://github.com/vicfergar/Floorplan3D/releases/download/v0.3-alpha/app.zip -O /tmp/app.zip && \
    unzip /tmp/app.zip -d /app && \
    rm /tmp/app.zip && \
    apt-get remove -y wget unzip && apt-get autoremove -y && apt-get clean

ENV ASPNETCORE_URLS=http://0.0.0.0:8099

EXPOSE 8099

ENTRYPOINT ["dotnet", "Floorplan3D.Web.Server.dll"]
