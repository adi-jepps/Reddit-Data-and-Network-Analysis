# Reddit Network Analysis of r/InvestmentClub

## Project Overview

This project presents an in-depth **network analysis of the r/InvestmentClub subreddit**, a Reddit community dedicated to financial discussions, investment strategies, and stock market insights. By leveraging data science techniques such as **graph theory**, **NLP**, **sentiment analysis**, and **community detection**, the project uncovers how information flows, who influences discussions, and what themes dominate over time.

---

##  Objectives

- Analyze user interaction patterns within the r/InvestmentClub subreddit.
- Identify and evaluate **superusers** and their role in shaping discussions.
- Use **community detection** algorithms to understand user clustering.
- Perform **sentiment analysis** and correlate it with real-world financial events.
- Extract and interpret **discussion topics** via Named Entity Recognition (NER).
- Examine **temporal trends** in user engagement and topic evolution.

---

##  Dataset Description

### Submissions (`submissions_1000.csv`)
- Each row corresponds to a Reddit post.
- Key fields:
  - `id`, `title`, `selftext`, `author`, `created_datetime`, `num_comments`, `score`, `ups`, `downs`, `url`

### Comments (`comments_1000.csv`)
- Each row corresponds to a comment or reply.
- Key fields:
  - `id`, `body`, `author`, `created_datetime`, `score`, `ups`, `downs`, `link_id`, `parent_id`, `controversiality`

### Custom Stopwords
- Provided in `stopwordFile.txt`
- Removes domain-specific non-informative words (e.g., "ups", "username", "said")

---

##  Methodology

### 1. **Data Cleaning and Merging**
- Removed null and irrelevant fields.
- Created structured relationships between comments and their parents using `parent_id` and `link_id`.
- Merged comment replies with post titles and filtered by comment score (threshold ≥ 5).

### 2. **Network Construction**
- **Directed Graph** built using `networkx`:
  - Nodes: users (blue), posts (red), superusers (yellow)
  - Edges: comment replies (user-to-user) and comment-post links (user-to-post)

### 3. **Centrality & Superuser Analysis**
- Calculated:
  - **Degree Centrality** – users with the most direct interactions
  - **Betweenness Centrality** – users bridging different communities
- Identified top 5% as **superusers**
- Measured network fragmentation with and without superusers

### 4. **Rich Club Coefficient**
- Analyzed connectivity of high-degree nodes.
- Users with degree ≥10 formed a tightly knit "rich club" (coefficient ≈ 1.0).

### 5. **Community Detection**
- Applied **Louvain algorithm** to detect sub-communities.
- Mapped each user to a cluster.
- Measured cluster engagement using combined comment and submission metrics.

### 6. **Natural Language Processing**
- Preprocessing:
  - Used spaCy (`en_core_web_sm`) and custom stopwords.
- Extracted **Named Entities** (ORG, GPE, PERSON, etc.)
- Identified discussion themes by community:
  - Common entities: *Warren Buffett*, *JPMorgan*, *Microsoft*, *China*, *NYSE*, *COVID-19*

### 7. **Sentiment Analysis**
- Used **VADER** to calculate compound sentiment scores.
- Temporal sentiment trends analyzed from 2012–2022.
- Correlated sentiment shifts with financial events:
  - 2015 China Market Crash
  - 2020 COVID-19 Crash
  - 2021 GameStop Squeeze

---

##  Key Insights

- **Superusers** act as central hubs and bridges; removing them increases network fragmentation by 2.4x.
- **Rich Club Formation** at degree ≥10 confirms elite user connectivity.
- **Community structures** are inclusive; superusers span across clusters rather than forming isolated elites.
- **Sentiment volatility** matches global market events and investor sentiment cycles.
- **Discussion themes** evolve from company performance to geopolitical risk as markets fluctuate.

---
##  Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/reddit-network-analysis.git
cd reddit-network-analysis
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

### 3. Run the analysis notebook
Open and run the Jupyter notebook ```Reddit Data and Network Analysis.py``` to reproduce the analysis and visualizations.

---

## Requirements

See `requirements.txt`. Main packages:
- `pandas`, `numpy`, `networkx`, `matplotlib`, `seaborn`
- `plotly`, `python-louvain`, `nltk`, `spacy`, `vaderSentiment`, `scikit-learn`

---

##  Future Enhancements

- Integrate **real-time Reddit streaming** using `PRAW` or `Pushshift` API.
- Incorporate **deep learning sentiment models** (e.g., BERT).
- Compare **multiple subreddits** to generalize financial community patterns.

---

##  Author

**Adithi Jeppu**  
Student ID: 3041073J  
University of Glasgow

_Project submitted as part of advanced data science coursework._
