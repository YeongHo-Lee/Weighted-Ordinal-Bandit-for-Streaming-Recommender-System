![image](https://github.com/YeongHo-Lee/AICP_WONDERS/assets/77314467/22b0296c-c654-42c4-93b6-40e002961b5d)# Weighted Ordinal Bandit for Streaming Recommender System

**Coworking of UNIST SDMLAB**.

<a href="https://github.com/JerryKwon">Youngin Kwon</a>, <a href="https://github.com/YeongHo-Lee">Yeongho Lee</a>, Yejin Kim, Yeongjin Ko, Gi-Soo Kim 

##  :triangular_flag_on_post: Competition info

### :label: ​Name

2021 Artificial Intelligence Challengers Program (AICP)

### :mag: Objective

Developed a news article recommendation bandit algorithm that adapts to users' changing preferences

### :stopwatch: Timeline

Mar, 2021 - Dec 2021

## Process

### 1. Research on the contextual multi-armed bandit

- Contextual multi-armed bandit (CMAB) : Unlike traditional multi-armed bandit algorithm, each choice (arm) has a corresponding context ($x_{t,i}$). For example, a news article's classification, title, date, etc.
- LinUCB : An algorithm that assumes a linear model of each arm's reward expectation with a given context vector and makes decisions based on an upper confidence bound (UCB) on each arm's reward expectation.
- Thompson Sampling (LinTS) : An algorithm that assumes that each arm's reward expectation is a linear model with a given context vector, such as LinUCB, but makes decisions using the reward expectation of each arm obtained by sampling parameters from a posterior distribution estimated at each point in time by assuming that the parameters are random variables.

### 2. Chosing Data

- ** R6B - Yahoo! Front Page Today Module User Click Log Dataset, version 2.0 (300 MB)[[url]](https://webscope.sandbox.yahoo.com/catalog.php?datatype=r&did=54&guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAIeRtdeIJKedFa2IxC_XpB7RtDW9NiBKEGrACYYXfa47q-Hfi0rg1anD96sXDrK-RwnSsfDEOi_GcBGd_n1bt1KsI3D739hrCcQRkHabNqQcpAzqE6tci2Z3XHlBdskYwTHMF9kzpEr8uOzQVR2F55v8UGC8qWSoya672QQPjFhP)
- Data is collected on whether a user with a random feature (displayed_arm) clicks on a news article (reward=1) or not (reward=0) with equal probability on a randomly displayed news article (displayed_arm) from a given set of news articles (pool) at a given point in time on the Yahoo front page.

### 3. Proposed Algorithm
- 
