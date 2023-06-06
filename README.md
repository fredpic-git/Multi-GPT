# Multi-GPT: Multiple Collaborating ExpertGPTs

## ⚠️IMPORTANT⚠️ Are you excited about the LLM/AI space? We want to hear from you! Click here to learn more: https://join.sid.ai/

> ***”Individually, we are one drop. Together, we are an ocean.”*** - Ryunosuke Satoro
>

![GitHub Repo stars](https://img.shields.io/github/stars/rumpfmax/multi-gpt?style=social)
[![Twitter Follow](https://img.shields.io/twitter/follow/md_rumpf?style=social)](https://twitter.com/md_rumpf)

Multi-GPT is an experimental multi-agent system. Multiple "expertGPTs" collaborate to perform a task. Each with their own short and long-term memory and the ability to communicate with each other.
### Demo (17/04/2023):

https://www.loom.com/share/b6bec93065794eb8a47e2109697afa39

## Table of Contents

- [Multi-GPT: Multiple Collaborating ExpertGPTs](#multi-gpt-multiple-collaborating-expertgpts)
    - [Demo (17/04/2023):](#demo-17042023)
  - [Table of Contents](#table-of-contents)
  - [🚀 Features](#-features)
  - [📋 Requirements](#-requirements)
  - [💾 Installation](#-installation)
  - [🔧 Usage](#-usage)
    - [Logs](#logs)
    - [Docker](#docker)
    - [Command Line Arguments](#command-line-arguments)
  - [🔍 Google API Keys Configuration](#-google-api-keys-configuration)
    - [Setting up environment variables](#setting-up-environment-variables)
  - [Memory Backend Setup](#memory-backend-setup)
    - [Redis Setup](#redis-setup)
    - [🌲 Pinecone API Key Setup](#-pinecone-api-key-setup)
    - [Milvus Setup](#milvus-setup)
    - [Weaviate Setup](#weaviate-setup)
    - [Setting up environment variables](#setting-up-environment-variables-1)
  - [Setting Your Cache Type](#setting-your-cache-type)
  - [View Memory Usage](#view-memory-usage)
  - [⚠️ Limitations](#️-limitations)
  - [🛡 Disclaimer](#-disclaimer)
  - [🐦 Connect with Us on Twitter](#-connect-with-us-on-twitter)
  - [Run tests](#run-tests)
  - [Run linter](#run-linter)

## 🚀 Features

- 🤯 Set a task and watch the experts get to work.
- 🌐 Internet access for searches and information gathering
- 💾 Long-Term and Short-Term memory management
- 🧠 GPT-4 instances for text generation
- 🔗 Access to popular websites and platforms
- 🗃️ File storage and summarization with GPT-3.5

## 📋 Requirements

- environments(just choose one)
  - [vscode + devcontainer](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers): It has been configured in the .devcontainer folder and can be used directly
  - [Python 3.10 or later](https://www.tutorialspoint.com/how-to-install-python-in-windows)
- [OpenAI API key](https://platform.openai.com/account/api-keys)

Optional:

- Memory backend
  - [PINECONE API key](https://www.pinecone.io/) (If you want Pinecone backed memory)
  - [Milvus](https://milvus.io/) (If you want Milvus as memory backend)
- ElevenLabs Key (If you want the AI to speak)

## 💾 Installation

To install Multi-GPT, follow these steps:

1. Make sure you have all the **requirements** listed above, if not, install/get them

_To execute the following commands, open a CMD, Bash, or Powershell window by navigating to a folder on your computer and typing `CMD` in the folder path at the top, then press enter._

2. Clone the repository: For this step, you need Git installed. Alternatively, you can download the zip file by clicking the button at the top of this page ☝️

```bash
git clone https://github.com/rumpfmax/Multi-GPT.git
```

3. Navigate to the directory where the repository was downloaded

```bash
cd Multi-GPT
```

4. Install the required dependencies

```bash
pip install -r requirements.txt
```

5. Locate the file named `.env.template` in the main `/Multi-GPT` folder.
   Create a copy of this file, called `.env` by removing the `template` extension.  The easiest way is to do this in a command prompt/terminal window `cp .env.template .env`
   Open the `.env` file in a text editor.  Note: Files starting with a dot might be hidden by your Operating System.
   Find the line that says `OPENAI_API_KEY=`.
   After the `"="`, enter your unique OpenAI API Key (without any quotes or spaces).
   Enter any other API keys or Tokens for services you would like to utilize.
   Save and close the `".env"` file.
   By completing these steps, you have properly configured the API Keys for your project.
   
  - See [OpenAI API Keys Configuration](#openai-api-keys-configuration) to obtain your OpenAI API key.
  - Obtain your ElevenLabs API key from: https://elevenlabs.io. You can view your xi-api-key using the "Profile" tab on the website.
  - If you want to use GPT on an Azure instance, set `USE_AZURE` to `True` and then follow these steps:
    - Rename `azure.yaml.template` to `azure.yaml` and provide the relevant `azure_api_base`, `azure_api_version` and all the deployment IDs for the relevant models in the `azure_model_map` section:
      - `fast_llm_model_deployment_id` - your gpt-3.5-turbo or gpt-4 deployment ID
      - `smart_llm_model_deployment_id` - your gpt-4 deployment ID
      - `embedding_model_deployment_id` - your text-embedding-ada-002 v2 deployment ID
    - Please specify all of these values as double-quoted strings
    ```yaml
    # Replace string in angled brackets (<>) to your own ID
    azure_model_map:
      fast_llm_model_deployment_id: "<my-fast-llm-deployment-id>"
      ...
    ```
    - Details can be found here: https://pypi.org/project/openai/ in the `Microsoft Azure Endpoints` section and here: https://learn.microsoft.com/en-us/azure/cognitive-services/openai/tutorials/embeddings?tabs=command-line for the embedding model.

## 🔧 Usage

1. Run `multigpt` Python module in your terminal

```
python -m multigpt
```

2. After each action, choose from options to authorize command(s),
exit the program, or provide feedback to the AI.
   1. Authorize a single command, enter `y`
   2. Authorize a series of _N_ continuous commands, enter `y -N`
   3. Exit the program, enter `n`


### Logs

Activity and error logs are located in the `./output/logs`

To print out debug logs:

```
python -m multigpt --debug
```

## OpenAI API Keys Configuration

Obtain your OpenAI API key from: https://platform.openai.com/account/api-keys.

To use OpenAI API key for Auto-GPT, you NEED to have billing set up (AKA paid account).

You can set up paid account at https://platform.openai.com/account/billing/overview.

![For OpenAI API key to work, set up paid account at OpenAI API > Billing](./docs/imgs/openai-api-key-billing-paid-account.png)


## 🔍 Google API Keys Configuration

This section is optional, use the official google api if you are having issues with error 429 when running a google search.
To use the `google_official_search` command, you need to set up your Google API keys in your environment variables.

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. If you don't already have an account, create one and log in.
3. Create a new project by clicking on the "Select a Project" dropdown at the top of the page and clicking "New Project". Give it a name and click "Create".
4. Go to the [APIs & Services Dashboard](https://console.cloud.google.com/apis/dashboard) and click "Enable APIs and Services". Search for "Custom Search API" and click on it, then click "Enable".
5. Go to the [Credentials](https://console.cloud.google.com/apis/credentials) page and click "Create Credentials". Choose "API Key".
6. Copy the API key and set it as an environment variable named `GOOGLE_API_KEY` on your machine. See setting up environment variables below.
7. [Enable](https://console.developers.google.com/apis/api/customsearch.googleapis.com) the Custom Search API on your project. (Might need to wait few minutes to propagate)
8. Go to the [Custom Search Engine](https://cse.google.com/cse/all) page and click "Add".
9. Set up your search engine by following the prompts. You can choose to search the entire web or specific sites.
10. Once you've created your search engine, click on "Control Panel" and then "Basics". Copy the "Search engine ID" and set it as an environment variable named `CUSTOM_SEARCH_ENGINE_ID` on your machine. See setting up environment variables below.

_Remember that your free daily custom search quota allows only up to 100 searches. To increase this limit, you need to assign a billing account to the project to profit from up to 10K daily searches._

### Setting up environment variables

For Windows Users:

```bash
setx GOOGLE_API_KEY "YOUR_GOOGLE_API_KEY"
setx CUSTOM_SEARCH_ENGINE_ID "YOUR_CUSTOM_SEARCH_ENGINE_ID"
```

For macOS and Linux users:

```bash
export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"
export CUSTOM_SEARCH_ENGINE_ID="YOUR_CUSTOM_SEARCH_ENGINE_ID"
```

## Setting Your Cache Type

By default, Auto-GPT is going to use LocalCache instead of redis or Pinecone.

To switch to either, change the `MEMORY_BACKEND` env variable to the value that you want:

* `local` (default) uses a local JSON cache file
* `pinecone` uses the Pinecone.io account you configured in your ENV settings
* `redis` will use the redis cache that you configured
* `milvus` will use the milvus cache that you configured
* `weaviate` will use the weaviate cache that you configured

### Redis Setup
> _**CAUTION**_ \
This is not intended to be publicly accessible and lacks security measures. Therefore, avoid exposing Redis to the internet without a password or at all
1. Install docker desktop
```bash
docker run -d --name redis-stack-server -p 6379:6379 redis/redis-stack-server:latest
```
> See https://hub.docker.com/r/redis/redis-stack-server for setting a password and additional configuration.

2. Set the following environment variables
> Replace **PASSWORD** in angled brackets (<>)
```bash
MEMORY_BACKEND=redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=<PASSWORD>
```
You can optionally set

```bash
WIPE_REDIS_ON_START=False
```

To persist memory stored in Redis

You can specify the memory index for redis using the following:

```bash
MEMORY_INDEX=<WHATEVER>
```

### 🌲 Pinecone API Key Setup

Pinecone enables the storage of vast amounts of vector-based memory, allowing for only relevant memories to be loaded for the agent at any given time.

1. Go to [pinecone](https://app.pinecone.io/) and make an account if you don't already have one.
2. Choose the `Starter` plan to avoid being charged.
3. Find your API key and region under the default project in the left sidebar.

In the `.env` file set:
- `PINECONE_API_KEY`
- `PINECONE_ENV` (example: _"us-east4-gcp"_)
- `MEMORY_BACKEND=pinecone`

Alternatively, you can set them from the command line (advanced):

For Windows Users:

```bash
setx PINECONE_API_KEY "<YOUR_PINECONE_API_KEY>"
setx PINECONE_ENV "<YOUR_PINECONE_REGION>" # e.g: "us-east4-gcp"
setx MEMORY_BACKEND "pinecone"
```

For macOS and Linux users:

```bash
export PINECONE_API_KEY="<YOUR_PINECONE_API_KEY>"
export PINECONE_ENV="<YOUR_PINECONE_REGION>" # e.g: "us-east4-gcp"
export MEMORY_BACKEND="pinecone"
```

### Milvus Setup

[Milvus](https://milvus.io/) is a open-source, high scalable vector database to storage huge amount of vector-based memory and provide fast relevant search.

- setup milvus database, keep your pymilvus version and milvus version same to avoid compatible issues.
  - setup by open source [Install Milvus](https://milvus.io/docs/install_standalone-operator.md)
  - or setup by [Zilliz Cloud](https://zilliz.com/cloud)
- set `MILVUS_ADDR` in `.env` to your milvus address `host:ip`.
- set `MEMORY_BACKEND` in `.env` to `milvus` to enable milvus as backend.
- optional
  - set `MILVUS_COLLECTION` in `.env` to change milvus collection name as you want, `autogpt` is the default name.


### Weaviate Setup
[Weaviate](https://weaviate.io/) is an open-source vector database. It allows to store data objects and vector embeddings from ML-models and scales seamlessly to billion of data objects. [An instance of Weaviate can be created locally (using Docker), on Kubernetes or using Weaviate Cloud Services](https://weaviate.io/developers/weaviate/quickstart). 
Although still experimental, [Embedded Weaviate](https://weaviate.io/developers/weaviate/installation/embedded) is supported which allows the Auto-GPT process itself to start a Weaviate instance. To enable it, set `USE_WEAVIATE_EMBEDDED` to `True` and make sure you `pip install "weaviate-client>=3.15.4"`. 

#### Setting up environment variables

In your `.env` file set the following:

```
MEMORY_BACKEND=weaviate
WEAVIATE_HOST="127.0.0.1" # the IP or domain of the running Weaviate instance
WEAVIATE_PORT="8080" 
WEAVIATE_PROTOCOL="http"
WEAVIATE_USERNAME="your username"
WEAVIATE_PASSWORD="your password"
WEAVIATE_API_KEY="your weaviate API key if you have one"
WEAVIATE_EMBEDDED_PATH="/home/me/.local/share/weaviate" # this is optional and indicates where the data should be persisted when running an embedded instance
USE_WEAVIATE_EMBEDDED=False # set to True to run Embedded Weaviate
MEMORY_INDEX="multigpt" # name of the index to create for the application
```
 
## View Memory Usage

1. View memory usage by using the `--debug` flag :)


## 🧠 Memory pre-seeding

# python autogpt/data_ingestion.py -h 
usage: data_ingestion.py [-h] (--file FILE | --dir DIR) [--init] [--overlap OVERLAP] [--max_length MAX_LENGTH]

Ingest a file or a directory with multiple files into memory. Make sure to set your .env before running this script.

options:
  -h, --help               show this help message and exit
  --file FILE              The file to ingest.
  --dir DIR                The directory containing the files to ingest.
  --init                   Init the memory and wipe its content (default: False)
  --overlap OVERLAP        The overlap size between chunks when ingesting files (default: 200)
  --max_length MAX_LENGTH  The max_length of each chunk when ingesting files (default: 4000)

# python autogpt/data_ingestion.py --dir seed_data --init --overlap 200 --max_length 1000
This script located at autogpt/data_ingestion.py, allows you to ingest files into memory and pre-seed it before running Auto-GPT. 

Memory pre-seeding is a technique that involves ingesting relevant documents or data into the AI's memory so that it can use this information to generate more informed and accurate responses.

To pre-seed the memory, the content of each document is split into chunks of a specified maximum length with a specified overlap between chunks, and then each chunk is added to the memory backend set in the .env file. When the AI is prompted to recall information, it can then access those pre-seeded memories to generate more informed and accurate responses.

This technique is particularly useful when working with large amounts of data or when there is specific information that the AI needs to be able to access quickly. 
By pre-seeding the memory, the AI can retrieve and use this information more efficiently, saving time, API call and improving the accuracy of its responses. 

You could for example download the documentation of an API, a GitHub repository, etc. and ingest it into memory before running Auto-GPT. 

⚠️ If you use Redis as your memory, make sure to run Auto-GPT with the `WIPE_REDIS_ON_START` set to `False` in your `.env` file.

⚠️For other memory backend, we currently forcefully wipe the memory when starting Auto-GPT. To ingest data with those memory backend, you can call the `data_ingestion.py` script anytime during an Auto-GPT run. 

Memories will be available to the AI immediately as they are ingested, even if ingested while Auto-GPT is running.

In the example above, the script initializes the memory, ingests all files within the `/seed_data` directory into memory with an overlap between chunks of 200 and a maximum length of each chunk of 4000.
Note that you can also use the `--file` argument to ingest a single file into memory and that the script will only ingest files within the `/auto_gpt_workspace` directory.

You can adjust the `max_length` and overlap parameters to fine-tune the way the docuents are presented to the AI when it "recall" that memory:

- Adjusting the overlap value allows the AI to access more contextual information from each chunk when recalling information, but will result in more chunks being created and therefore increase memory backend usage and OpenAI API requests.
- Reducing the `max_length` value will create more chunks, which can save prompt tokens by allowing for more message history in the context, but will also increase the number of chunks.
- Increasing the `max_length` value will provide the AI with more contextual information from each chunk, reducing the number of chunks created and saving on OpenAI API requests. However, this may also use more prompt tokens and decrease the overall context available to the AI.

## 💀 Continuous Mode ⚠️

Run the AI **without** user authorization, 100% automated.
Continuous mode is NOT recommended.
It is potentially dangerous and may cause your AI to run forever or carry out actions you would not usually authorize.
Use at your own risk.

1. Run the `multigpt` python module in your terminal:

```bash
python -m multigpt --speak --continuous
```

2. To exit the program, press Ctrl + C

## GPT3.5 ONLY Mode

If you don't have access to the GPT4 api, this mode will allow you to use Auto-GPT!

```bash
python -m multigpt --speak --gpt3only
```

It is recommended to use a virtual machine for tasks that require high security measures to prevent any potential harm to the main computer's system and data.

## 🖼 Image Generation

By default, Auto-GPT uses DALL-e for image generation. To use Stable Diffusion, a [Hugging Face API Token](https://huggingface.co/settings/tokens) is required.

Once you have a token, set these variables in your `.env`:

```bash
IMAGE_PROVIDER=sd
HUGGINGFACE_API_TOKEN="YOUR_HUGGINGFACE_API_TOKEN"
```

## Selenium
```bashOkay that's good what can you actually want you to close that a sister and a dog eat quietly and don't need to cross I love is there an option
sudo Xvfb :10 -ac -screen 0 1024x768x24 & DISPLAY=:10 <YOUR_CLIENT>
```

## ⚠️ Limitations

This experiment aims to showcase the potential of GPT-4 but comes with some limitations:

1. Not a polished application or product, just an experiment
2. May not perform well in complex, real-world business scenarios. In fact, if it actually does, please share your results!
3. Quite expensive to run, so set and monitor your API key limits with OpenAI!

## 🛡 Disclaimer

Disclaimer
This project, Auto-GPT, is an experimental application and is provided "as-is" without any warranty, express or implied. By using this software, you agree to assume all risks associated with its use, including but not limited to data loss, system failure, or any other issues that may arise.

The developers and contributors of this project do not accept any responsibility or liability for any losses, damages, or other consequences that may occur as a result of using this software. You are solely responsible for any decisions and actions taken based on the information provided by Auto-GPT.

**Please note that the use of the GPT-4 language model can be expensive due to its token usage.** By utilizing this project, you acknowledge that you are responsible for monitoring and managing your own token usage and the associated costs. It is highly recommended to check your OpenAI API usage regularly and set up any necessary limits or alerts to prevent unexpected charges.

As an autonomous experiment, Auto-GPT may generate content or take actions that are not in line with real-world business practices or legal requirements. It is your responsibility to ensure that any actions or decisions made based on the output of this software comply with all applicable laws, regulations, and ethical standards. The developers and contributors of this project shall not be held responsible for any consequences arising from the use of this software.

By using Auto-GPT, you agree to indemnify, defend, and hold harmless the developers, contributors, and any affiliated parties from and against any and all claims, damages, losses, liabilities, costs, and expenses (including reasonable attorneys' fees) arising from your use of this software or your violation of these terms.

## 🐦 Connect with Us on Twitter

Stay up-to-date with the latest news, updates, and insights about Multi-GPT by following our Twitter accounts. Engage with the developer and the AI's own account for interesting discussions, project updates, and more.

- **Developer**: Follow [@md_rumpf](https://twitter.com/md_rumpf) for insights and updates. Also follow [@SigGravitas](https://twitter.com/SigGravitas) for updates on AutoGPT.
- **Sponsors**: Please also follow our founding sponsor [@try_sid](https://twitter.com/try_sid) on Twitter.

## Run tests

To run tests, run the following command:

```bash
python -m unittest discover tests
```

To run tests and see coverage, run the following command:

```bash
coverage run -m unittest discover tests
```

## Run linter

This project uses [flake8](https://flake8.pycqa.org/en/latest/) for linting. We currently use the following rules: `E303,W293,W291,W292,E305,E231,E302`. See the [flake8 rules](https://www.flake8rules.com/) for more information.

To run the linter, run the following command:

```bash
flake8 multigpt/ autogpt/ tests/

# Or, if you want to run flake8 with the same configuration as the CI:
flake8 multigpt/ autogpt/ tests/ --select E303,W293,W291,W292,E305,E231,E302
```
