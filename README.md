# private-chat-with-pdf
Using completely private tools to create a PDF chatbot 


# Implementation

We're using the HuggingFace **Text Generation Inference** tool ([link](https://github.com/huggingface/text-generation-inference)) to load LLM models and serve for production.

The easiest way to get it up and running is to use the `docker run ...` command. The full command can be found in the documentation itself. First time you run the docker command, it may take a while until it downloads the model. It's very important to specify the `/data` directory in your local, so that you don't have to download the model every time you run the container.

For this example, we're going to use the **Falcon 7B** model. But, you can use any other model supported by the **Text Generation Inference** tool. Here's the docker command for inferencing with the **Falcon 7B** model:

```bash
docker run --platform linux/amd64 --gpus all --shm-size 1g -p 8080:80 -v $PWD/data:/data ghcr.io/huggingface/text-generation-inference:0.9.1 --model-id OpenAssistant/falcon-7b-sft-top1-696 --num-shard 1
```

**Note:** In case you are using Apple Silicon Mx chips, you need to use the `--platform linux/amd64` flag to run the container.

**Note:** If you don't have GPU, you can remove the `--gpus all` flag.

To run the chatbot, run `python bot.py --fname <your PDF file name>` in CLI.