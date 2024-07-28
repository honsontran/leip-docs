---
tags:
  - "#installation"
  - "#getting-started"
  - tutorials
  - lre
custom-width: .nan
---
# Prerequisites
Before installation, ensure your device is supported. You can reference our [[Latent Runtime Engine (LRE)|Supportability Matrix]].
# Step 1: Get Access to Latent AI Packages

> [!TIP] Tip  
> You can make `LICENSE_KEY` and `LEIP_WORKSPACE` persist for every new `bash` session by placing the variables in `~/.bashrc`.

In order to install packages, you'll need to create a personal access token. To do so, follow these steps:

1. Login to [Latent AI Artifact repository](https://repository.latentai.com/)
    - Click the `Sign-in` link in the upper right
    - Select `Sign-in with SSO`
    - Enter your access credentials
2. Create your Personal Access Token
    - Click on your profile in the upper right
    - Select `User Token` on the left navigation
    - Select the `Access User Token` button
    - View your user token name and user token passcode
3. Export your user token name and passcode.
	```bash
	REPOSITORY_TOKEN_NAME=<token_name>
	REPOSITORY_TOKEN_PASS=<token_value>
	```
# Step 2: Install [[Latent Runtime Engine (LRE)|LRE]] on Target Hardware

> [!bug] Bug
> There's a current issue with `pip install pylre[liblre]` installing `pylre==0.0.3`. You still need `pylre[liblre` regardless of this.
> 
> As a workaround, install `pylre[liblre]` first, then run `pip install pylre==1.0.0`.

Proceed with installation on your edge device by opening up a terminal session and following the steps below.
1. Add the Latent AI packaged repository.
	```bash
	sudo wget -qO - https://public.latentai.io/add_apt_repository | sudo bash
	```
2. Run `sudo apt update`. 
3. Install [[Latent Runtime Engine (LRE)|LRE]]. If your application is using Python, make sure you install [[PyLRE]] as well.
	```bash
	pip install --extra-index-url=https://$REPOSITORY_TOKEN_NAME:$REPOSITORY_TOKEN_PASS@repository.latentai.com/repository/pypi/simple pylre[liblre]
	```
# Step 3: A Simple [[PyLRE]] Test
You can do a simple [[PyLRE]] test