<div id="header" align="center">
<img src="https://github.com/user-attachments/assets/580b3d49-e431-4ac8-9fb2-712a0a077161" width="200"/>
</div>

---

### About the project:

Inify is a service for accounting and analytics of user assets in the world of web3 and cryptocurrencies.

The problem that our project solves: in web3 there are many different crypto wallets, exchanges and other means of viewing and managing your assets, our service helps the user collect and combine information from all means of storing assets into one whole and presents this information in the form of convenient statistics.

---

### Functionality and architecture:

1. Authorization and authentication. As well as full user account management.
2. Linking any number of wallets to a user account for further analytics.
3. Analytics of one or all wallets linked to a user account at the same time. The project directly interacts with the blockchain in real time to analyze user transactions and find out how much money he has in certain tokens and wallets.

UseCase diagram according to which the project was made:

![Untitled](https://github.com/user-attachments/assets/80eb60bc-10bf-4d78-a07e-2892a8dd5159)

First sketches of the interface:

![Untitled2](https://github.com/user-attachments/assets/67108f22-e6f1-439a-bce3-7673fc9d53ff)
![Untitled3](https://github.com/user-attachments/assets/ca2fbf6c-8b2e-479b-8544-25b29ec03646)
![Untitled4](https://github.com/user-attachments/assets/bc76208d-f13b-4d1b-917e-bb66cea4e14d)

Sequence diagram to understand how the main function of our application will work for analytics:

![Untitled5](https://github.com/user-attachments/assets/ca94d295-efde-4b79-916b-b2907481ee86)

Application architecture:

The project consists of 4 microservices:
- UsersMs (responsible for full user management)
- WalletsMs (manages wallets tied to the user)
- TokensMs (a microservice that automatically populates the database with tokens that our project can parse to create a whitelist and does not parse tokens that are created for divorce).
- BlockchainParsersMs (a microservice that parses the number and price of tokens in real time)

Diagram:

![Untitled6](https://github.com/user-attachments/assets/bb5868cd-ae63-418e-a815-85341f4b3d5a)

Technologies used to write the project
- Programming languages
  - C#
  - JavaScript
- Frameworks/libraries
  - ASP.NET
  - React
  - Nethereum
  - Third-party services
  - Infura (provides us with a node to send requests to the blockchain)
  - CoinMarketCap (provides us with a list of trusted tokens, as well as prices in USD per unit of a particular token)
- Development tools
  - GIT
  - Docker
  - Microsoft SQL Server
  - NuGet

---

### Deployment and first-run guide programs:

First you need to clone the repository with submodules using the command below or unzip the archive with the project to the desired folder.

```properties
git clone --recurse-submodules git@github.com:InifyOrg/Inify.git
```

Next, you need to go to the host of each microservice and build a Docker image for them using the commands below (this is not done in compose.yaml because it does not allow you to run a build with the -f flag, without which the image cannot be created)

1. Open the console in the main, first folder of the project

For the usersms microservice:
```properties
cd UsersMS/UsersMS.Host

docker build -f Dockerfile .. -t usersmshost

cd ..
cd ..
```

For the walletsms microservice:
```properties
cd WalletsMS/WalletsMS.Host

docker build -f Dockerfile .. -t walletsmshost

cd ..
cd ..
```

For the tokensms microservice:
```properties
cd TokensMS/TokensMS.Host

docker build -f Dockerfile .. -t tokensmshost

cd ..
cd ..
```

For blockchainparsersms microservice:
```properties
cd BlockchainParsersMS/BlockchainParsersMS.Host

docker build -f Dockerfile .. -t blockchainparsersmshost

cd ..
cd ..
```

For apigateway microservice:
```properties
cd ApiGateway/ApiGateway.Host

docker build -f Dockerfile .. -t apigatewayhost

cd ..
cd ..
```

2. From the main project folder, run the following command

```properties
docker compose up -d
```

and wait until the command finishes its work and compiles all containers.

3. When the container creation process is complete, check if they are working using the command

```properties
docker ps
```

if 7 containers are running, everything has started successfully and you can test.
