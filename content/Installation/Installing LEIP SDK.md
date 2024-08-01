---
tags:
  - installation
  - getting-started
  - tutorials
  - optimize
  - design
custom-width: .nan
---
> [!NOTE]  Note
> If you would like to schedule an evaluation of LEIP, please contact us at [support@latentai.com](mailto:support@latentai.com.)
# Step 1: Get Access to our Container Repository

> [!WARNING]  Skip this step if...
> You only need the user token if you are installing any Latent AI specific Python packages, such as the [[Latent Runtime Engine (LRE)]]. If you are installing entirely with Docker, use the `LICENSE_KEY` found in your email.

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
3. Login to our Docker repository. Then use the user credentials obtained from [[Installing LEIP SDK#Step 1 Get Access to our Container Repository]].
	```bash
	$ docker login repository.latentai.com
	Username: $REPOSITORY_TOKEN_NAME
	Password: $REPOSITORY_TOKEN_PASS
	```
### Method 1: Entirely Docker
The *easiest* way to install the LEIP SDK is by using `docker compose` to initialize both [[Design|LEIP Design]] and [[Optimize|LEIP Optimize]].

```bash
# Make sure you're in leip-tutorials/environment
docker compose up leip-af leip-cf
```

### Method 2: Local Environment with LEIP Optimize
WIP
# Step 3: Use LEIP
If you opted in for [[#Method 1 Entirely Docker|Method 1: Entirely Docker]], a Jupyter Notebook instance will automatically start.

You can access this notebook in your browser via http://127.0.0.1:8888. The Jupyter password is `leip`.

To get started with using LEIP, view our #tutorials .

Once you have optimized your model and you're ready for deployment, refer to [[Installing LRE]].