
# Automated Telegram News Channel using n8n and Ollama

## Overview

This n8n workflow automatically monitors Google News RSS feeds, summarizes news articles using a local Ollama large language model, categorizes each article, and posts clean news bulletins to a Telegram channel.
It also prevents duplicate news from being posted by storing processed items in an n8n Data Table.

## What This Workflow Does

1. Polls Google News RSS feed every seven minutes
2. Filters out already processed news items using a Data Table
3. Cleans the news title by removing publisher names
4. Summarizes the article into short numbered bullet points
5. Classifies the news into a single category
6. Stores the processed news in a Data Table
7. Publishes the formatted news post to a Telegram channel

## Workflow Architecture

Trigger
RSS Feed Trigger polls Google News

Processing
Title cleanup using Ollama
News summarization using Ollama
Category classification using Ollama

Deduplication
Checks GUID and link against an n8n Data Table

Storage
Stores GUID, link, title, category, and summarized content

Delivery
Sends formatted HTML message to a Telegram channel using Telegram Bot API

## Requirements

1. n8n version supporting Data Tables and LangChain nodes
2. Ollama installed and running locally
3. Mistral 7B model available in Ollama
4. Telegram Bot Token
5. Telegram Channel ID
6. Internet access for Google News RSS

## Required Credentials

Ollama API credentials configured in n8n
Telegram Bot Token added directly in the HTTP Request node

## Setup Instructions

1. Import the workflow JSON into n8n
2. Configure Ollama credentials in n8n
3. Ensure the Mistral 7B model is available in Ollama
4. Create an n8n Data Table named News with the following columns
   GUID
   Link
   Content
   Category
   Title
5. Replace YOUR_BOT_TOKEN in the HTTP Request node
6. Replace the Telegram channel ID with your own channel
7. Activate the workflow

## Telegram Message Format

Each message sent to Telegram includes
Bold title
Category label
Numbered key points
Read more link to the original article

## Categories Used

Politics
Business
Technology
Geopolitics
Sports
Entertainment
Science
Health
Other

Only one category is assigned per news item.

## Notes and Limitations

This workflow relies on Google News RSS structure
Summaries depend on the quality of the Ollama model output
High RSS volume may increase local model load
Duplicate detection depends on GUID and link consistency

## File

The workflow file included in this repository is
Automated Telegram News Channel.json

## License

Use freely and modify as needed.
No warranty is provided.

