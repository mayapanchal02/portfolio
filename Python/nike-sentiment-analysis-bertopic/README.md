# Sentiment Analysis of Nike Shoes Using BERTopic

## Overview
This project analyzes consumer sentiment and engagement for Nike’s sustainable versus non-sustainable footwear. Using web-scraped product data and customer reviews, we evaluate whether sustainability labeling influences customer satisfaction, demand, and sentiment. The analysis combines statistical testing with NLP-based topic modeling using BERTopic.

## Problem Statement
As sustainability becomes a growing focus in the fashion industry, companies face pressure to align environmental goals with consumer demand. This project examines whether customer sentiment and engagement differ between sustainable and non-sustainable Nike shoes, and whether product descriptions accurately reflect consumer experience.

## Data Collection
Because existing datasets were outdated, a custom dataset was created by web scraping Nike’s website using BeautifulSoup.

Collected features include:
- Product ID and URL  
- Full and discounted prices  
- Discount status  
- Product descriptions  
- Average rating scores  
- Number of reviews  
- Customer review text  

Shoes were classified as **sustainable** or **non-sustainable** based on Nike’s “Made with Sustainable Materials” labeling.

## Text Preprocessing
To prepare text data for analysis:
- All text was lowercased and normalized  
- Stop words were removed using NLTK  
- Tokens were lemmatized after part-of-speech tagging  
- Word frequency analysis was performed to identify common themes  

## Statistical Analysis
To assess differences in customer satisfaction and engagement:
- A **t-test** compared average ratings between sustainable and non-sustainable shoes  
- A **chi-square test** compared distributions of review counts  

Both tests produced non-significant results (p > 0.05), indicating no meaningful difference in ratings or engagement based on sustainability labeling alone.

## Topic Modeling with BERTopic
BERTopic was used to cluster product descriptions and customer reviews. The approach leverages:
- Transformer-based embeddings  
- UMAP for dimensionality reduction  
- HDBSCAN for clustering  
- Keyword extraction for topic interpretation  

After correcting an initial modeling assumption and retraining on the project dataset, results consistently highlighted themes related to **comfort, preference, quality, and performance** across both shoe categories.

## Key Findings
- Customer satisfaction and engagement are similar for sustainable and non-sustainable shoes  
- Comfort and preference dominate consumer sentiment regardless of sustainability  
- Product descriptions strongly align with customer reviews, suggesting effective marketing  
- Sustainability labeling does not negatively impact consumer perception or demand  

## Takeaways
- Consumers prioritize comfort and quality over sustainability labeling alone  
- Nike can expand sustainable product offerings without risking customer satisfaction  
- Greater transparency around materials and production could strengthen consumer trust  

## Limitations
- Review data may not capture opinions of customers who did not leave reviews  
- Sustainability impact was inferred through labeling rather than direct lifecycle analysis  

## Tools
Python, BeautifulSoup, Pandas, NumPy, NLTK, BERTopic, Matplotlib, SciPy


