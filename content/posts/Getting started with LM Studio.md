---
title: Getting started with LM Studio
date: 2024-11-29
draft: false
tags: ["Artificial Intelligence", "LM Studio", "Llama", "Local LLM", "Large Language Models", "ChatGPT", "GPT", "Chatbot"]
---
# 0X02 Getting started with LM Studio
For my next foray into the world of Artificial Intelligence I will be using LM Studio due to some information I've heard about the customization and power of using this specific platform. In a future blog post we will go over doing this with Ollama as well since it is another popular option.

---
## Downloading LM Studio
I went to the website: 
![LM Studio Website showing links to Windows, Mac, and Linux installation](/images/lmstudio.png)
I do not have a Mac computer so I will not be making a blogpost about downloading it on Mac, but you can see the option is there if you are running a Mac system.

After going to their site I pressed on the button to download, since I am using Windows currently I selected the "Download LM Studio for Windows" option, I am currently dual booting Windows and Linux (I only really keep Windows due to being a gamer), so I will eventually make a blog post about trying the AI applications on Linux to see if it is easier or rather more difficult, and if it performs better or the same.

It finished downloading:

![It is downloading LM Studio on the screen](/images/lmstudiodownload.png)

Generally I like to check for hash checksums on files I install from websites, but they did not appear to provide this option, and I can see the website is secure with an SSL certificate that links back to their company, so I am going to just install it this time.

---
## Installing LM Studio 

After running the executable and waiting for a bit I was brought to a screen: 

![I am going through the initial setup for LM Studio and it is asking to choose a model](/images/lmstudiosetup.png)

It was trying to get me to download the Llama 3.2 1B model, it didn't present any other options, so I skipped onboarding for now, will check what models they have available afterwards.

I've done a bit of research and decided upon starting with the Qwen2.5 Coder 14B model for LM Studio, as I feel like it could be useful for some of my intended purposes of the AI model. Which is to facilitate a Local LLM that I can use to assist in security research or with cybersecurity in general, and to ensure that I would not be funneling my data through some third party if this works well enough to replace my current setup.

---

## Exploring Qwen2.5 Coder 14B for Cybersecurity Applications  

After installing LM Studio, I wanted to start strong by diving into a model that could provide robust assistance with technical tasks. Based on my research, I settled on the **Qwen2.5 Coder 14B** model. This model is known for its high performance in tasks involving coding, troubleshooting, and technical analysis—making it particularly appealing for cybersecurity professionals and enthusiasts like me.  

### Why Qwen2.5 Coder 14B?  

Qwen2.5 Coder 14B stands out due to its specialization in coding-related tasks and its ability to handle complex problem-solving scenarios. Here are a few reasons I found it intriguing:  

- **Code Analysis**: This model can assist with reverse engineering, reviewing source code, and identifying vulnerabilities in software. For cybersecurity, that means faster audits and a second pair of "eyes" for catching weak points.  
- **Threat Intelligence**: By leveraging natural language queries, Qwen2.5 Coder can help parse logs, analyze patterns in attack vectors, and identify anomalies in a network's behavior.  
- **Automation**: With its capacity to generate scripts and troubleshoot issues in real-time, it could streamline repetitive tasks like configuring firewall rules or writing detection logic for SIEMs.  
- **CTF Help**: For Capture The Flag (CTF) challenges, it might be able to assist in solving challenges faster, especially for scripting puzzles or decoding obfuscated malware samples.  

### Cybersecurity Use Cases  

Here’s a breakdown of some practical ways to use Qwen2.5 Coder 14B in cybersecurity:  

1. **Malware Analysis**  
   - Feeding disassembled code or scripting elements into the model could help in identifying potential threats or offering explanations for obscure functions.  
   - It may also assist in generating YARA rules or deobfuscating code snippets found in the wild.  

2. **Incident Response**  
   - Imagine being able to quickly generate regex patterns for log parsing or automate steps in the investigation of phishing incidents. Qwen2.5 Coder could be a game changer here.  

3. **Red Team Operations**  
   - Need help writing a PowerShell script for lateral movement or a Python exploit for privilege escalation? This model can help get a draft ready.  
   - It can also simulate attacker behavior, providing a way to test your blue team's response.  

4. **Blue Team Defense**  
   - From generating Splunk queries to crafting custom detection rules for endpoint monitoring tools, the possibilities are endless.  
   - It might even assist with threat hunting by generating hypotheses for network anomalies.  

---

## Using LM Studio for the first time.


I downloaded the model and I waited for it to finish, after it finished I was met with this glorious screen:
![It is finished downloading the model and I am using it for the first time](/images/qwenstart.png)

I decided to use the same test that I used in my Chat RTX article, and see how it can explain and demonstrate SPF records.

It worked *really well.* I read it over and from what I can see and know about SPF records everything appears to be correct, it was able to explain it in a simple way that many people could understand, and it provided good examples that would be useable and help demonstrate how to use it to someone who has no idea what an SPF record is.
![An example of Qwen 2.5 Coder 14B Instruct handling a question about SPF records](/images/qwenspfexample.png)

Here is the full output to help explain:

---
## Output from requesting information about SPF

Sure! SPF stands for Sender Policy Framework. It's an email validation system designed to prevent email spoofing by verifying that the email sent from your domain originates from a legitimate server authorized by that domain.

Here’s a basic overview of how SPF works:

1. **DNS TXT Record**: You add a DNS TXT record to your domain’s DNS settings. This record specifies which mail servers are permitted to send emails on behalf of your domain.
2. **Email Sending**: When an email is sent from one of the authorized servers, it includes this information in the header.
3. **Receiving Server Check**: The receiving server then checks the SPF record for the sender’s domain against the IP address of the sending server. If the IP is listed as authorized, the email can be considered legitimate.

### Example of an SPF TXT Record

Let's say you have a domain `example.com` and your mail servers are located at `mail.example.com` and `smtp.example.org`. You want to ensure that only these servers can send emails on behalf of `example.com`.

Here’s what the SPF record might look like:

```
v=spf1 mx ip4:192.0.2.1 ip6:2001:DB8::1 include:_spf.google.com ~all
```

**Explanation of Components:**

- **`v=spf1`**: Specifies that this is an SPF version 1 record.
- **`mx`**: Indicates that the domain’s mail exchange (MX) servers are allowed to send email on behalf of `example.com`.
- **`ip4:192.0.2.1`** and **`ip6:2001:DB8::1`**: Allow specific IPv4 and IPv6 addresses.
- **`include:_spf.google.com`**: Includes Google’s SPF record, allowing any server listed there to send email on behalf of `example.com`.
- **`~all`**: Soft fail directive. If no match is found, the receiving mail server should treat it as "soft fail" and may still deliver the message but flag it as potentially spoofed.

### Steps to Set Up SPF

1. **Identify Sending Servers**: Determine all the IP addresses and domains of the servers that will send emails on behalf of your domain.
2. **Create TXT Record**: Construct an SPF record using the appropriate directives (`ip4`, `ip6`, `mx`, etc.) based on your sending server information.
3. **Add to DNS**: Add this TXT record to your domain’s DNS settings, usually via your registrar or hosting provider’s control panel.
4. **Test Configuration**: Use online tools to verify that your SPF record is correctly published and working.

### Example of a Complete SPF Record for `example.com`

```
v=spf1 mx ip4:192.0.2.3 ip4:198.51.100.6 include:mailserver.example.net ~all
```

In this example:
- **`mx`** allows the mail servers listed in `example.com`’s MX records.
- **`ip4:192.0.2.3` and `ip4:198.51.100.6`** specify two specific IP addresses that can send emails.
- **`include:mailserver.example.net`** allows any server listed in the SPF record of `mailserver.example.net`.
- **`~all`** acts as a soft fail for any other sending servers.

### Important Considerations

- **Hard Fail vs. Soft Fail**: Use `all` to strictly prevent unauthorized email (hard fail) or use `~all` to allow delivery but flag it as potentially spoofed (soft fail).
- **Update Regularly**: Ensure your SPF record is regularly updated as you add or remove sending servers.
- **Avoid Overlapping**: Make sure that there are no overlapping directives in your SPF record that might cause confusion.

By setting up an SPF record, you can help protect your domain from unauthorized email spoofing and improve the deliverability of legitimate emails.

---

This is the metric by which we tested the previous models in Chat RTX and it simply outperformed them. It used about the same amount of resources on my system, so it's not like it slowed my system down. This is revolutionary, and I think if it continues to perform like this then this will become an integral part of my technical toolset.
### Initial Impressions  

I’ve started playing around with Qwen2.5 Coder 14B, and I’m impressed with its contextual understanding of code and cybersecurity-related queries. While it’s not a replacement for expertise (and shouldn’t be blindly trusted—always validate!), it’s a fantastic co-pilot for anyone working in IT security.  

I’ll share a follow-up post soon with some real-world examples of how I’m applying Qwen2.5 Coder 14B to my own projects. For now, it’s safe to say this model has enormous potential for improving productivity in cybersecurity workflows. 

---
