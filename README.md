Fine-tune a Large Language Model (LLM) and deploy it on MonsterAPI 🔥

The best part - it costs less than a cup of coffee and requires no coding! 🔥



🧵 1/3

-----

@monsterapis designed their no-code LLM fine-tuner that simplifies the process of finetuning by:

👉 Automatically configuring GPU computing environments,

👉 Optimizing memory usage by finding the optimal batch size,

👉 Integrates experiment tracking with WandB, and

👉 Auto configures the pipeline to complete without any errors on their cost-optimised GPU cloud

📌 And all the above steps are without writing a single line of code.

📌 Recently, they finetuned Mistral-7B using the "no-robots" dataset and the finetuned model outperformed the base model on various benchmarks. The entire model finetuning cost was less than a cup of coffee.

-----

The actual process for Finetuning an LLM

📌 Launch a Finetuning Portal, and choose from the latest Large Language Models (LLMs) such as Llama 2 7B, CodeLlama, Falcon, GPT-J 6B or X-Gen.

📌 Dataset Preparation: You can choose from the curated selection of mostly used hugging face datasets with predefined training prompt configuration. OR

You can use your own custom datasets, and we get a good amount of control around how the Dataset needs to be prepared in the right format. The portal provides a text-area in which target columns can be specified. Depending on the type of task chosen, you might need to alter the column names.

📌 Specify Hyperparameter Configuration: such as epochs, learning rate, cutoff length, warmup steps, and so on.

📌 Track stages of your finetuning jobs: Like, view job logs, monitor your job metrics using Weights & Biases. And finally upload model outputs to Hugging Face.

------

📌 Once you have finetuned an LLM on MonsterAPI, you will receive adapter weights as the final output. This adapter contains your fine-tuned model’s weights that Monster will host as an API endpoint using Monster Deploy.

📌 MonsterDeploy optimizes its backend operations using vLLM framework. vLLM is a rapid and user-friendly library for large language model inference and serving, notable for its state-of-the-art serving throughput.

------

👉 Website : http://monsterapi.ai

👉 Discord (Monsterapis) : https://discord.com/invite/mVXfag4kZN

👉 Access all Finetuned Models by Monster here:

https://huggingface.co/qblocks?ref=blog.monsterapi.ai


![](assets/2024-01-18-22-27-14.png)


##################################################

## 2nd Tweet

##################################################

🧵 2/3

The example code in the image, deploys the Mixtral 8x7b Chat model with GPTQ 4bit quantization with a 48GB GPU through Monster Deploy.

The Deployment will be able to serve the model as a REST API for both static and streaming token response support.


![](assets/2nd-Tweet.png)


#######################################################

## 3rd Tweet

#######################################################

🧵 3/3

Once the deployment is live, let's query the deployed LLM endpoint:

![](assets/3rd-Tweet.png)