
# Zoho Cliq Bot with OpenAI (ChatGPT) Integration

This repository provides a Deluge script that integrates a Zoho Cliq Bot with OpenAI (ChatGPT). Using Zoho's Data Store, the script maintains conversation history, allowing for more context-aware responses in both group and direct (one-on-one) conversations.

## Table of Contents

- [Zoho Cliq Bot with OpenAI (ChatGPT) Integration](#zoho-cliq-bot-with-openai-chatgpt-integration)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
  - [Configuration](#configuration)
  - [Creating the Zoho Cliq Bot](#creating-the-zoho-cliq-bot)
  - [Setting Up the Handlers](#setting-up-the-handlers)
  - [Usage](#usage)
  - [License](#license)
  - [Contributing](#contributing)
  - [Disclaimer](#disclaimer)
  - [Questions or Support](#questions-or-support)

---

## Overview

**What this is**: A Deluge script to connect your Zoho Cliq Bot to OpenAI's GPT-based models. It allows you to:
- Store chat history in a Zoho Data Store to maintain context based conversations with ChatGPT via API.
- Maintain context for both group channels and direct messages independently.
- Adjust parameters (model, temperature, etc.) for your OpenAI calls.

**Why this is useful**: You can create custom chatbots within Zoho Cliq that leverage OpenAI's large language models. The bot will remember recent messages in each channel or conversation, enabling more coherent and context-aware interactions.

---

## Prerequisites

1. **Zoho Cliq Administrator and Zoho Developer Experience**  
   - You need permissions to create or edit a bot in Zoho Cliq.
   - You will need to be comfortable with editing Deluge scripts.

2. **OpenAI Account and API Key**  
   - Sign up at [OpenAI's platform](https://platform.openai.com/) if you haven't yet.
   - Create an API key under your **API Keys** section.
   - You will need to add a payment method to your OpenAi Platform account and add credits. OpenAi charges for the use of their API be careful of your usage and the costs involved.

---

## Configuration

The key configuration parameters in the script are:

1. **OpenAI API Settings**  
   ```Deluge
   openaiApiKey = "<ADD YOUR OPENAI API KEY HERE>";
   openaiEndpoint = "https://api.openai.com/v1/chat/completions";
   defaultOpenAIModel = "gpt-4o";
   defaultTemperature = 0.7;
   defaultMaxTokens = 1000;
   defaultTopP = 1;
   defaultFreqPenalty = 0;
   defaultPresPenalty = 0;
   ```
   - `openaiApiKey`: Your OpenAI API key (paste your secret key here).
   - `defaultOpenAIModel`: Which ChatGPT model you’d like to use (e.g., `"gpt-3.5-turbo"` or `"gpt-4"`).
   - `defaultTemperature`: Controls the "creativity" of responses (range is usually `0.0` to `1.0`).
   - `defaultMaxTokens`: Max tokens for the model to generate in one response.
   - `defaultTopP`, `defaultFreqPenalty`, `defaultPresPenalty`: Other standard OpenAI settings to control text generation parameters.

2. **Conversation Size Limits**  
   ```Deluge
   maxMessagesGroup = 40;
   maxMessagesDM = 20;
   ```
   - `maxMessagesGroup`: How many messages to keep in conversation history for channels.
   - `maxMessagesDM`: How many messages to keep for direct (one-on-one) chats.

3. **System Message**  
   ```Deluge
   systemMessageContent = "<ADD YOUR SYSTEM MESSAGE HERE>";
   ```
   - Sets the initial context/instructions for the bot that influences all subsequent responses.

---

## Creating the Zoho Cliq Bot

1. **Go to Zoho Cliq** -> **Bots** -> **Create Bot**.
2. Give your bot a name, an icon, and a description.
3. Define the bot’s function scopes/permissions as needed (e.g., ability to post to channels, read messages, etc.).
4. Once your bot is created, you’ll have the option to add or edit **Message Handler** and **Mention Handler**.

---

## Setting Up the Handlers

By default, Zoho Cliq provides rudimentary scripts for the bot’s **Message Handler** and **Mention Handler**. 

1. **Copy the Deluge script from this repository**.
2. Replace the default code in both the **Message Handler** and **Mention Handler** with the script.
3. Make sure to update the configuration section at the top (API Key, system message, etc.) to match your environment.
4. Save your changes.

---

## Usage

- **In a Group (Channel or Thread)**: When a user mentions the bot (if configured that way) or posts a message that triggers the bot, the script will capture the conversation context in `chatbotconversations` under a key prefixed with `GROUP_`. Set to 40 messages by default.
- **In a Direct Message**: Similarly, any conversation is captured under a key prefixed with `DM_`. Set to 20 messages by default.
- **The bot responds** based on the OpenAI Chat Completion API response. Each time it replies, it appends the assistant's response to the conversation list and saves it in the data store, preserving context.

To reset the conversation, simply remove the data store entry for that conversation key or modify the logic as needed.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## Disclaimer

Use at your own risk and be mindful of any data you submit to the OpenAI API, which is governed by OpenAI's own terms of service. Always safeguard confidential information. OpenAi API costs money to use, and will require a payment method to be set up and credits to be added, be mindful of your usage and the costs involved.

---

## Questions or Support

If you encounter any issues, you can reach out via the Zoho community forums.

