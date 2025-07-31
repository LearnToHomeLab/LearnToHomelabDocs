# Actual Budgeting

In this episode we are going to cover a budgeting app called Actual. It is open source and totally free. If you would like to review screenshots of what it looks like and to learn more, check it our [here](https://actualbudget.org/docs/tour/user-interface)

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Y3viBQ8TR0Q?si=rnHTrnmsJBBt7CEC" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
## Prerequisites

You will need to have some way of forcing HTTPS for this application to work. If you are following our homelab series, you would have already set up the Nginx Proxy Manager and that is what we are using in this video. If you need to install that first, follow our tutorial [here](https://www.learntohomelab.com/homelabseries/EP26_nginxproxymanagerssl/)

## Install Docker/Docker Compose

First thing we need to do is install docker and docker compose.

We will be following the documentation found [here](https://docs.docker.com/engine/install/ubuntu/)

See the following commands to install Docker:

Run the following command to uninstall all conflicting packages:

```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

Set up Docker's `apt` repository.

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install the Docker packages.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify that the installation is successful by running the `hello-world` image:

```
sudo docker run hello-world
```

Verify the compose version:

```
docker compose version
```

## Create a compose file

To use Docker Compose, you need to create a `compose.yaml` which will hold the configuration for running the Vaultwarden container.

```
nano compose.yml
```

Then you paste the following configuration:

```
services:
  actual_server:
    image: docker.io/actualbudget/actual-server:latest
    ports:
      # This line makes Actual available at port 5006 of the device you run the server on,
      # i.e. http://localhost:5006. You can change the first number to change the port, if you want.
      - '5006:5006'
    volumes:
      # Change './actual-data' below to the path to the folder you want Actual to store its data in on your server.
      # '/data' is the path Actual will look for its files in by default, so leave that as-is.
      - ./actual-data:/data
    healthcheck:
      # Enable health check for the instance
      test: ['CMD-SHELL', 'node src/scripts/health-check.js']
      interval: 60s
      timeout: 10s
      retries: 3
      start_period: 20s
    restart: unless-stopped
```

Start the Docker Compose file with (the -d runs it in the background so you can still use your CLI:)

```
docker compose up -d
```

Grab the IP address of the machine with the following command:

```
ip a
```

Now navigate to your browser and type the following in to go to Actual:

If you do not know your server IP you can type _ip a_ into the cli to find it.

```
 http://localhost:5006
```

## Force HTTPS with Nginx Proxy Manager

Next thing you will need to do is login to your Nginx Proxy Manager and add Actual to it. If you are unsure how to do this, you can follow our video on how to do that [here](https://www.learntohomelab.com/homelabseries/EP26_nginxproxymanagerssl/)

## Login to Actual

Actual will only require a password to login. You can start fresh or video demo, I would recommend you view the demo to get started faster.

## How to Budget with Acutal

If you would like to read more on how to budget with Actual and understand its concepts to budgeting, that can be found [here](https://actualbudget.org/docs/budgeting/)

## Importing Bank Transactions

Instead of importing all your transactions you can setup a connection to SimpleFIN Bridge for American users which can be found [here](https://beta-bridge.simplefin.org/) and only 15 USD per year.

For our European viewers you can use GoCardless which you can learn more about [here](https://actualbudget.org/docs/advanced/bank-sync/)

## Using Credit Cards

Many people including me get confused on how to use a credit card with a budgeting app, that is why I wanted to make a specific section covering this topic. I will also cover how to do this in future videos. You can find how to use your credit card with your budget [here](https://actualbudget.org/docs/budgeting/credit-cards/)

## Updating Actual

To update actual you can do it with the following commands:

To check what version you are on and see the uptime you can do:

```
docker compose ps
```

To pull the latest you can do

```
docker compose pull
```

Then to recreate and start the container you can do

```
docker compose up -d
```

## How to use Actual

First thing, DO NOT OVERCOMPLICATE. You NEED obvious categories. The more categories you have, the easier it is to make balancing your budget impossible! Also, set up all your categories first!

Remember, we should not create a category for each item. I will give you an example: You will not have a category called mortgage, to then just pay your mortgage. That complicates things and makes projections for future months harder. You will take all recurring bills and slap them in the SAME category. At the end of the day, the bills themselves don’t matter; what matters is knowing you have 3K in bills and need 3K in income to zero out that category. Give each dollar a job, paying off something.

### Paying Credit Card Transactions

Many people ask how to categorize credit card payoff transactions (moving money from your checking account to pay off your credit card balance). We simply create a new group called “Credit Card Payments” and assign those transactions there.

As for the line item of what you bought on the credit card, this is still set to the category, food, bills, etc.

### Bought and returned goods

To keep your balance sheet accurate, you may buy something, then categorize it. Well, a few weeks or days go by, and you return it, you may add that money as income, right? Wrong, you will add that item to the same category as your initial purchase, which will equal out your balance sheet between categories and keep your account correct.

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)