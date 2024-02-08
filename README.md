🤔 Thinking of deploying a Large Language Model (LLM) in production with low-cost and low-complexity ❓

✨ Monster-API may just be the answer - gateway to seamlessly deploy LLMs and docker containers on its robust GPU compute infrastructure.

✨ Quickly get an API endpoint that can start serving text generation requests using models like Llama2 7B, CodeLlama 34B, Falcon 40B or any of your custom/finetuned models.

✨ Developed with the vLLM (Variably-Large Language Models) project as its foundation, the Deploy service is optimized for high throughput.

✨ As per their official blog, they were able to serve Zephyr-7b, a SOTA Open source 7B param LLM, at an incredibly economical rate of $1.25/hr, serving 39K requests per hour with an average request latency of 16ms on a 24GB GPU.

And this was using Monster Deploy on GPUs such as Nvidia RTX A5000 (24GB)  and A100 (80GB).

@monsterapis

📌 Seamless experience with its intuitive UI

📌 Python client or a single curl request.

📌 Supports deployment of LLMs as a REST API endpoint and any custom docker image as a hosted docker container.

📌 Choose from a range of GPU and RAM configurations upto 160GB of VRAM

📌 Detailed API documentations with demo notebook.

👉 Website : https://monsterapi.ai

🧵 1/3

=================================


🧵 1/3

To access Monster Deploy Beta:

Step 1: Sign up on MonsterAPI platform.
Step 2: Apply for Monster Deploy Beta. Use your organization/business email for free 30K credits.

=================================

The example code in image, deploys the Mixtral 8x7b Chat model with GPTQ 4bit quantization by using a 48GB GPU, using Monster Deploy.

The Deployment will be able to serve the model as a REST API for both static and streaming token response support.

Signup Here - https://developer.monsterapi.ai/docs/monster-deploy-beta#beta-phase--feedback

```py
!python3 -m pip install monsterapi==1.0.2b3
# install specific beta version of client for quick serve access.

api_key = "YOUR_MONSTER_API_KEY"
from monsterapi import client as mclient
deploy_client = mclient(api_key = api_key)

# deploy Mixtral 8x7b Chat model with GPTQ 4bit quantization
# using a 48GB GPU.
basemodel_path="TheBloke/Mixtral-8x7B-Instruct-v0.1-GPTQ"
    prompt_template="<s> [INST] {instruction} [/INST] {completion}</s>"
    api_auth_token="A_RANDOM_AUTH_TOKEN_TO_SECURE_YOUR_ENDPOINT"
    per_gpu_vram=48
    gpu_count=1

# Launch a deployment
launch_payload = {
    "basemodel_path": "TheBloke/Mixtral-8x7B-Instruct-v0.1-GPTQ",
    "prompt_template": "<s> [INST] {prompt} [/INST] {completion}</s>",
    "api_auth_token": "b6a97d3b-35d0-4720-a44c-59ee33dbc25b",
    "per_gpu_vram": 48,
    "gpu_count": 1,
    "use_nightly": True
}

# Launch a deployment
ret = deploy_client.deploy("llm", launch_payload)
deployment_id = ret.get("deployment_id")
print(deployment_id)
"""
{
     "status":"live",
     "message":"Server has started !!!",
     "URL":"https://c503a813-850a-4a78-93b9.monsterapi.ai",
     "api_auth_token":"57b7b903-a4b6-4720-8154-af71aa8e8313"
 }
 visit the url to get the llm service endpoint details
 or above url/docs to get swagger docs
"""

```

=================================

Once the deployment is live, let's query our deployed LLM endpoint

```py
import json

status_debug = True # Just a placeholder to show possible statuses.

if status_debug:
  status_ret = deploy_client.get_deployment_status(deployment_id)
  print(status_ret)

assert status_ret.get("status") == "live", "Please wait until status is live!"

service_client  = mclient(api_key = status_ret.get("api_auth_token"),
                          base_url = status_ret.get("URL"))

payload = {
    "input_variables": {
        "prompt": "What's up?"},
    "stream": False,
    "temperature": 0.6,
    "max_tokens": 2048
}

output = service_client.generate(model = "deploy-llm", data = payload)

if payload.get("stream"):
    for i in output:
        print(i[0])
else:
    print(json.loads(output)['text'][0])

```

=================================
=================================


🧵 1/3

Below we showcase a benchmark of serving Zephyr-7b, a SOTA Open source 7B parameter LLM, using Monster Deploy on GPUs such as Nvidia RTX A5000 (24GB)  and A100 (80GB) in multiple scenarios.


=================================

🧵 1/3

As a result, we were able to serve this LLM at an incredibly economical rate of $1.25/hr, serving 39K requests per hour with an average request latency of 16ms on a 24GB GPU

![](assets/2024-02-08-18-22-04.png)

=================================

Cost For Different Scenarios

![](assets/2024-02-08-18-22-17.png)

===================

API Docs of Monster-Deploy - https://developer.monsterapi.ai/docs/monster-deploy-beta

👉 Discord (Monsterapis) : https://discord.com/invite/mVXfag4kZN

👉 Chat with their Finetuned Model here (Mistral-7b-No-robots Finetunned LLM)

https://huggingface.co/spaces/qblocks/chat-mistral-7b-norobots
