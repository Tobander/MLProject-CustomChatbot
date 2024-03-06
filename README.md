# 🔴 What is a Custom Chatbot?

## Problem
Today on so many websites, intranet sites or blogs there are search bars, that are either not giving any results or results that don't really capture what the user is asking. That is neither the user's nor the search bar's fault. It is more often just a problem of formulating the problem. Normally you are able to type in just a few words in a search bar. However, it would be much easier to describe your problem, what are you searching for or what you are interested in. Like you would talk to a real person.

Also most sites use basic **search algorithms** that lack the sophistication of major search engines like Google or Bing. These algorithms may not effectively parse natural language queries or understand the context of the search, leading to less relevant results.

The way content is **organized and tagged** (or the lack thereof) significantly impacts search effectiveness as well. If the content on the site is not properly categorized or tagged with relevant metadata, the search engine may struggle to index and retrieve the most relevant documents or pages.

What makes finding relavant information on some websites more challenging than a simple Google search for example, is that most users are accustomed to the **efficiency of modern internet search engines** and may have expectations that an simple Website, Blog or Intranet search cannot meet due to its more limited resources and scope.

Also if the website's search engine does not frequently **update its index** or if certain areas are not indexed at all, users may not be able to find newly added content or specific types of content.

## Solution
A Chatbot has the ability to have a **natural conversation** with the user and if it has the knowledge of the whole Website, Intranet or Blog can then give the user great recommendations. The user doesn't have to guess specific keywords or phrases that the search engine might recognize.

They can also understand the **context of a query**, allowing them to provide more accurate and relevant responses. They can remember the context of a conversation over multiple interactions, refining their search results based on the ongoing dialogue.

It's also **time saving** because the user doesn't have to sift through a list of search results but get the answer, link or product with the most relevant content based on the user's query.  

## How To
First we need to get the information from our target website. The **knowledge** of our Chatbot so to speak. Most of the time this is done by scraping the website. Just make sure that you are not violating data privacy and/or store personal information without consent.

Then we need to put this data into an easy to read format. Most of the time this will be a JSON format but a database or other flat file formats can also make sense.

The next thing is to get the **embeddings** for our data which means converting our products, articles or knowledge into vectors of numbers in a way that captures their meanings, relationships, or characteristics. To do this, we use OpenAI's `text-embedding-3-small` model. We will also get the embeddings of the user's input (his question). When comparing these two, we can find the best product, article or whatever your use-case is for the user's question. One commonly used method to do this comparison is the cosine similarity. It ranges from -1 to 1, where 1 means the vectors are in the same direction (very similar), 0 means they are orthogonal (not similar), and -1 means they are in opposite directions (very dissimilar).

The last thing we need to do is calling our **chat model** with the user's input and hand-over the information we have just selected from our database (or JSON file) so it can use it to answer the question. To do this, we use OpenAI's latest model `gpt-4-0125-preview` which is like it's predecessor optimized for Chat.

So here are the basic steps visualized:

![slide](https://github.com/Tobander/MLProject-CustomChatbot/assets/45336196/1a45c5c8-ddde-47be-88b3-47135c867abc)

# 🟢 Building the database or JSON file
First thing we need to do is build the knowledge of our Chatbot. Meaning the products of your Online-Store or the guidlines and documents of your Intranet or the articles of your Blog. Most of the time the easiest way to do this, is to scrape the information. Again, please make sure beforehand that you are not violating any personal rights. 

For our Chatbot example I am using <a href="https://books.toscrape.com/index.html">Books to Scrape</a> which is a demo website for web scraping purposes. We are going to collect all Book titles and their product information like category, price, rating or if they are in stock and save everything in a JSON file.

📓 **Notebook:** You can find the complete code in `scrape_website.ipynb`

# 🟢 Get the Embeddings for the JSON file
Up next we need to get the Embeddings for our data which is a vector (list) of floating point numbers. The distance between two vectors measures their relatedness. Small distances suggest high relatedness and large distances suggest low relatedness.

To get an Embedding, we send our complete product data to OpenAI's embeddings API endpoint and we will use it's latest model which is called `text-embedding-3-small`. The response will contain an Embedding which we then then also save in our JSON file. 

By default, the length of the embedding vector will be 1536, so our product data will significantly grow in size in this step.

📓 **Notebook:** You can find the complete code in get_embeddings.ipynb
