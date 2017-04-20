FROM microsoft/dotnet


RUN apt-get -qq update && apt-get -qqy --no-install-recommends install \
    git \
    unzip

RUN curl -sL https://deb.nodesource.com/setup_6.x |  bash -
RUN apt-get install -y nodejs

# install bower
RUN npm install --global bower

RUN echo '{ "allow_root": true }' > /root/.bowerrc

RUN npm install -g gulp

WORKDIR /webapp

COPY . .

RUN dotnet restore

# copy and build everything else
RUN dotnet build --configuration "Release"
RUN dotnet publish -c Release -o out
ENTRYPOINT ["dotnet", "out/WebApplication.dll"]
EXPOSE 5000