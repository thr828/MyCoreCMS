FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base 
EXPOSE 8089
WORKDIR /web                 
COPY . ./
ENTRYPOINT ["dotnet", "MyCMS.Web.dll"] 