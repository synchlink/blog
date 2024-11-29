# Chatting Smarter with RTX Integration

11/28/2024

## Understanding LLMs and Tokens  

Most readers are likely already familiar with the concept of LLMs (Large Language Models). In today’s world, it’s hard not to be at least indirectly aware of AI, especially in the form of LLMs. For those with only a limited understanding of this concept, let’s start with a brief introduction before diving into the main topic of this post.  

An **LLM** is a type of artificial intelligence designed to process and generate human-like text by analyzing vast amounts of data. Essentially, these models learn patterns, context, and relationships within language, enabling them to perform tasks ranging from generating simple text to solving complex problems. Think of them as advanced tools capable of writing essays, answering questions, or simulating conversations, all while adapting to the user’s tone and style. Unlike systems that are merely programmed with static answers, LLMs “learn” from their training data, making their responses dynamic and contextually aware. Whether through chatbots, search engines, or creative applications, LLMs are rapidly becoming integral to how we interact with technology.  
## Popular Platforms for Interacting with LLMs  

There are many platforms available for interacting with an LLM, each offering unique features and capabilities. Some of the most well-known include:  

1. **OpenAI’s ChatGPT**  
   OpenAI’s ChatGPT has set the standard for conversational AI, offering a user-friendly interface that makes it accessible to individuals and businesses alike. It’s highly versatile, supporting a wide range of tasks, from drafting emails to coding assistance, all while maintaining a conversational tone. OpenAI also offers API access, enabling developers to integrate LLM capabilities into their own applications.  

2. **Meta’s LLaMA**  
   Meta’s LLaMA (Large Language Model Meta AI) is an open-source model designed with a focus on accessibility for researchers and developers. While less polished in user-facing tools compared to ChatGPT, LLaMA’s open nature allows for deep customization and experimentation, making it a favorite among AI enthusiasts and those seeking to build tailored solutions.  

3. **Google’s Gemini**  
   Google’s Gemini brings a unique perspective to the table, often integrating tightly with Google’s ecosystem of tools and services. Known for its focus on multilingual capabilities and advanced reasoning, Gemini aims to tackle complex tasks like scientific research, providing accurate and efficient results. If you’re already tied into Google’s ecosystem, this could be an ideal option.  

4. **openrouter.ai**  
   OpenRouter.ai acts as a unified platform, allowing users to route queries to multiple LLMs from different providers. This flexibility is particularly useful for comparing outputs or leveraging the strengths of various models without switching between platforms. It’s a great choice for those who want the best of all worlds, whether for research, development, or simply exploring AI’s capabilities.  

Each of these platforms caters to slightly different needs and audiences, so choosing the right one often depends on your specific goals. Are you looking for simplicity and ease of use? Go with ChatGPT. Do you want an open playground for customization? LLaMA might be your pick. Need tight integration into your productivity tools? Gemini could be perfect. Or, if you can’t decide, openrouter.ai offers the flexibility to experiment with multiple options in one place.  

No matter which platform you choose, the possibilities for leveraging LLMs are vast and growing every day.  

However, using these online LLM services comes with limitations—chiefly, the number of tokens you can use. If you’re not familiar with how LLMs operate, you might be asking:  

**What exactly are tokens?**  

Let’s take this opportunity to explore and clarify this important concept.  


## Tokens
Tokens, at their core, are the smallest units of text that a language model processes. On a low level, this involves breaking down input text into smaller components—sometimes individual characters, other times whole words or subwords, depending on the model's design. In hardware terms, processing these tokens requires memory allocation, computational power, and optimized storage for quick access. Each token is represented as a sequence of numbers (vectors) that the model uses to predict the next token or generate an appropriate response. The efficiency of this tokenization process directly impacts the performance and speed of the model, particularly on high-powered GPUs and TPUs designed to crunch vast amounts of numerical data in real time.

When interacting with online language models, tokens take on a more practical significance, especially in terms of cost. Many providers charge based on the number of tokens processed during a session—both the tokens in your input and the tokens generated in the output. For instance, if you input a 100-word query and the model generates a 200-word response, the total cost would depend on how these words are split into tokens, which may number several hundred in total. This token-based pricing model incentivizes users to craft concise queries while still achieving the desired result. Understanding token limits is also crucial, as models often have maximum token counts for input and output, which can restrict the complexity of the tasks they can handle.

Another important consideration is how tokens impact context and memory. In many LLMs, the total number of tokens determines how much information the model can "remember" within a single interaction. This context window governs the model’s ability to maintain coherence, track topics, or refer back to earlier parts of the conversation. If you exceed this token limit, older parts of the interaction are truncated or lost, which can lead to incomplete or disjointed responses. Recognizing this limitation is key when designing prompts or workflows to ensure your interactions remain logical and productive.

I’ve decided to dive into running local LLMs on my system. Naturally, I’m planning to explore several different approaches to make this happen—Ollama being one of the main ones on my list. But with my shiny new Nvidia RTX 4070 Ti SUPER freshly installed, I thought, _why not kick things off with Chat RTX?_ It feels like the perfect way to put this beast of a GPU to the test.

And that's where we are now with this blog post, so I went to the website: 
https://www.nvidia.com/en-us/ai-on-rtx/chatrtx/

I started the download for the NVIDIA ChatRTX, however the file is 10GB and my internet is not the best sometimes, in my experiences browsers notoriously fail when downloading large files if your internet is not fast enough to download it quickly. So, I am using an application called J Downloader 2.

![Picture of J Downloader, the download page](/images/jdownloader.png)
[J Downloader 2 download page](https://jdownloader.org/download/index)

And I start the download of the file:
![Picture that shows how long the download will take, it says it will take over an hour](/images/download.png)

Definitely going to need a coffee break.

It took a little while to complete but I was able to successfully download the installer.

I sat and asked a few questions to see if it could come up with accurate information I also have a screenshot of my task manager on the left to show how this is consuming my system resources:

![image of the performance of the mistral AI bot on the chatrtx interface](/images/mistral.png)
At first the answer is satisfactory and seems to accurate describe what an SPF (Sender Policy Framework) record is. However, when you ask it to create or explain it to you, it does not provide usable results. The information it provided was wrong, v=spf1 -all does not say that every single mail server is authorized to send on your behalf, it means that no one is. So, so far the "Mistral" model in ChatRTX was not satisfactory in the accuracy of its results. I also noted that there was literally no memory of previous contact with the LLM. Every response had no recollection of previous responses, so it could be talking about SPF and cut off, then you ask it to continue and it says "Sure, what would you like me to continue?"

I am currently installing Llama2 13B int4 and I will test that one out to see how it performs, if I am able to get it to run on my system. This model outperforms the previous one certainly, it is able to output more information, and it also provided accurate information. It perhaps oversimplified certain things. But, overall this was a greater response.
![Picture of the Llama2 13B model performing on the question of what is a SPF record](/images/llama2.png)
And unfortunately it does not have good memory either:
![Shows the poor memory performance of the ChatRTX models.](/images/llama21.png)
That's going to be it for now. I wasn't impressed enough with the chat with files feature. I'm going to look more into it and see if I can figure it out better before presenting it. Overall, I'm not too keen on ChatRTX, and I will try ollama next time when I do an Artificial Intelligence post about running local LLM's.

Thank you for reading and I hope you were able to get something from this.