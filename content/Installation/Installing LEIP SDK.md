---
tags:
  - installation
  - getting-started
  - tutorials
  - optimize
  - design
custom-width: 100
---
> [!NOTE]  Note
> If you would like to schedule an evaluation of LEIP, please contact us at [support@latentai.com](mailto:support@latentai.com.)
# Step 1: Access our Container Repository
In order to install packages or pull any of our Docker images, you'll need to create a personal access token. To do so, follow these steps:
1. Login to [Latent AI Artifact repository](https://repository.latentai.com/).
    - Click the `Sign-in` link in the upper right.
    - Select `Sign-in with SSO`.
    - Enter your access credentials.
2. Create your Personal Access Token.
    - Click on your profile in the upper right.
    - Select `User Token` on the left navigation.
    - Select the `Access User Token` button.
    - View your user token name and user token passcode.
3. Export your user token name and passcode.
	```bash
	REPOSITORY_TOKEN_NAME=<token_name>
	REPOSITORY_TOKEN_PASS=<token_value>
	```
# Step 2: Install LEIP SDK

> [!TIP] Tip  
> You can make `LICENSE_KEY` and `LEIP_WORKSPACE` persist for every new `bash` session by placing the variables in `~/.bashrc`.

There are two components to the LEIP SDK, [[Design|LEIP Design]] and [[Optimize|LEIP Optimize]].

There is also two methods of installing the SDK. Depending on your path ([[Bring Your Own Data (BYOD)]] or [[Bring Your Own Model (BYOM)]]), you will either just need 
## Prerequisites
Regardless of your installation method, make sure you configure the following:

1. Clone `leip-tutorials` and go into the `environment` directory.
	```bash
	git clone https://github.com/latentai/leip-tutorials.git
	cd leip-tutorials/environment
	```
2. `export` the following system variables:
	* `LICENSE_KEY` - You should have received this via email.
	* `LEIP_WORKSPACE` - The default path where all artifacts are placed as you use the SDK.
	``` bash
	export LICENSE_KEY=key/<license_key>
	export LEIP_WORKSPACE=/path/to/leip-tutorials/notebooks
	```
3. Login to our Docker repository. Then use the user credentials obtained from [[Installing LEIP SDK#Step 1 Access our Container Repository]]. You'll have to manually copy and paste the variables listed below.
	```bash
	$ docker login repository.latentai.com
	Username: $REPOSITORY_TOKEN_NAME
	Password: $REPOSITORY_TOKEN_PASS
	```
### Method 1: Entirely Docker
The *easiest* way to install the LEIP SDK is by using `docker compose` to initialize both [[Design|LEIP Design]] and [[Optimize|LEIP Optimize]].

```bash
# Make sure you're in leip-tutorials/environment
# -d is to automatically detach from the container after initialzation
docker compose up -d leip-af leip-cf
```

### Method 2: Local Environment with LEIP Optimize
WIP
# Step 3: Use LEIP
If you opted in for [[#Method 1 Entirely Docker|Method 1: Entirely Docker]], a Jupyter Notebook instance will automatically start.

You can access this notebook in your browser via http://127.0.0.1:8888. The Jupyter password is `leip`.

To get started with using LEIP, view our #tutorials .

Once you have optimized your model and you're ready for deployment, refer to [[Installing LRE]].

---
# Additional Configurations
These are additional configurations in the even the default instructions above need to be modified.
## Use LEIP via SSH
If you have deployed LEIP on a remote instance or server, you can tunnel the Jupyter instance back to your local machine with either method below.
### Inline Terminal Command
```bash
ssh -L your_local_port:localhost:8888 user@ip_address
```
### Stored as an SSH Bookmark
You can store these SSH settings in `~/.ssh/config`:
```bash
Host bookmark_name
    User your_username
    HostName ip_address_here
    Port 22
    LocalForward your_local_port 127.0.0.1:8888
```

Then, simply type in `ssh bookmark_name` to connect.
## Using Different Ports for [[What is LEIP?|LEIP]]

> [!NOTE]  
> If you are interacting with [[What is LEIP?|LEIP]] by sending commands from outside the Docker containers, use the port you defined in `CHANGE_LOCAL_PORT_TO_ACCESS_LEIP_CF` when a URL is required. However, if you are utilizing [[What is LEIP?|LEIP]] with our `docker compose` files, the containers are referencing the internal port `8888`.

In the event you need to use different ports for [[What is LEIP?|LEIP]], make the following changes to the YAML file in `leip-tutorials/environment`.
### `docker-compose.cpu.yml`
```
networks:
	...

volumes:
	...

services:
	leip-cf:
		...
		...
		ports:
			- CHANGE_LOCAL_PORT_TO_ACCESS_LEIP_CF:8888
		...

	leip-af:
		...
		...
		ports:
			- CHANGE_LOCAL_PORT_TO_JUPYTER_NOTEBOOK:8888
		...
```
## Changing the Docker Virtual Network Name for LEIP
Change the network name in the following YAML file in `leip-tutorials/environment`.
### `docker-compose.yml`
```
networks:
  default:
    name: CHANGE_NETWORK_NAME_HERE

volumes:
	...
```
## Spawning Multiple LEIP Instances
In the event you need to have multiple LEIP instances on a single server, make sure to:
* Change the ports mentioned in [[#Using Different Ports for LEIP]] to avoid port conflict with other [[What is LEIP?|LEIP]] instances during initialization.
* Change the virtual network name in [[#Changing the Docker Virtual Network Name for LEIP]] to avoid network name conflicts during initialization.

Once those steps are done, start an instance with the `-p` flag to add a prefix to the beginning of the container names. This will create create the containers needed with the prefix in front to avoid container name conflicts with other [[What is LEIP?|LEIP]] instances.

```bash
docker compose -p new_user up -d leip-af leip-cf
```

The command above will spawn containers named `new_user-leip-af` and `new_user-leip-cf`.