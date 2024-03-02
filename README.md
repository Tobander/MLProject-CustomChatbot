# 🔴 What is a Custom Chatbot?

## Problem
Today on so many websites, intranet sites or blogs there are search bars, that are either not giving any results or results that don't really capture what the user is asking. That is neither the user's nor the search bar's fault. It is mnore often just a problem of formulating the problem. Normally you are able to type in just a few words in a search bar. However, it would be much easier to describe your problem, what are you searching for or what you are iunterested in. Like you would talk to a real person.

## Solution
A Chatbot has the ability to have a **natural conversation** with the user and if it has the knowledge of the whole website, intranet or blog can then give the user great recommendations.

## How To
First we need to get the information from our target website. The **knowledge** of our Chatbot so to speak. Most of the time this is done by scraping the website. Just make sure that you are not violating data privacy and/or store personal information without consent.

Then we need to put this data into an easy to read format. Most of the time this will be a JSON format but a database or other flat file formats can also make sense.

The next thing is to get the **embeddings** for our data which means converting our products, articles or knowledge into vectors of numbers in a way that captures their meanings, relationships, or characteristics. To do this, we use OpenAI's `text-embedding-3-small` model. We will also get the embeddings of the user's input (his question). When comparing these two, we can find the best product, article or whatever your use-case is for the user's question. One commonly used method to do this comparison is the cosine similarity. It ranges from -1 to 1, where 1 means the vectors are in the same direction (very similar), 0 means they are orthogonal (not similar), and -1 means they are in opposite directions (very dissimilar).

The last thing we need to do is calling our **chat model** with the user's input and hand-over the information we have just selected from our database (or JSON file) so it can use it to answer the question. To do this, we use OpenAI's latest model `gpt-4-0125-preview` which is like it's predecessor optimized for Chat.

So here are the basic steps visualized:

<img width="870" alt="Workflow Custom Chatbot" src="https://github.com/Tobander/MLProject-CustomChatbot/assets/45336196/96f5dac3-1acb-47d0-a5b6-883cb23af242">
