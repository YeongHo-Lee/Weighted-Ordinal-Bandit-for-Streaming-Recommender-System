# Weighted Ordinal Bandit for Streaming Recommender System(WONDERS)

**TEAM WONDERS**.

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

- Contextual multi-armed bandit (CMAB) : Unlike traditional multi-armed bandit algorithm, each choice (arm) has a corresponding context ($x_{t,i}$). For example, a news article's classification, title, date, etc.[[pdf]](https://dl.acm.org/doi/pdf/10.1145/1772690.1772758)
- LinUCB : An algorithm that assumes a linear model of each arm's reward expectation with a given context vector and makes decisions based on an upper confidence bound (UCB) on each arm's reward expectation.[[pdf]](https://proceedings.neurips.cc/paper/2011/file/e1d5be1c7f2f456670de3d53c7b54f4a-Paper.pdf)
- Thompson Sampling (LinTS) : An algorithm that assumes that each arm's reward expectation is a linear model with a given context vector, such as LinUCB, but makes decisions using the reward expectation of each arm obtained by sampling parameters from a posterior distribution estimated at each point in time by assuming that the parameters are random variables.[[pdf]](http://proceedings.mlr.press/v28/agrawal13.pdf)

### 2. Choosing Data

- **R6B - Yahoo! Front Page Today Module User Click Log Dataset, version 2.0 (300 MB)** [[url]](https://webscope.sandbox.yahoo.com/catalog.php?datatype=r&did=54&guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAIeRtdeIJKedFa2IxC_XpB7RtDW9NiBKEGrACYYXfa47q-Hfi0rg1anD96sXDrK-RwnSsfDEOi_GcBGd_n1bt1KsI3D739hrCcQRkHabNqQcpAzqE6tci2Z3XHlBdskYwTHMF9kzpEr8uOzQVR2F55v8UGC8qWSoya672QQPjFhP)
- Data is collected on whether a user with a random feature (displayed_arm) clicks on a news article (reward=1) or not (reward=0) with equal probability on a randomly displayed news article (displayed_arm) from a given set of news articles (pool) at a given point in time on the Yahoo front page.
- ![image](https://github.com/YeongHo-Lee/AICP_WONDERS/assets/77314467/dcbf69d2-8a05-416f-8d50-3396ce832e89)
- ![image](https://github.com/YeongHo-Lee/AICP_WONDERS/assets/77314467/c280f9e7-def0-4fa6-8bc0-bde21f6bd466)


### 3. Proposed Algorithm
- weight $0 \leq w_t \leq 1$ : Define queues as large as window size ($w$) to reflect changing preferences. Queue only news articles with positive rewards to learn which news articles users prefer. The average value of the cosine distance (1-cosine similarity ($S_c$)) between the selected news article and the queued favourite news article is used as a weighting factor, with higher weighting if the selected news article is different from the favourite news article
- Learn the Weighted Least Squares method for weighting LinUCB and LinTS : $\hat{\theta}=\argmin_{\theta}\sum_{i=1}^Nw_i(y_i-x_i'\theta)^2 
\Rightarrow \hat{\theta}_{WLS}=(X^TWX)^{-1}X^TWY$
- Performance issues with the Thompson Sampling method : As the dimensionality of the estimated parameters for the bandit algorithm increased, the performance of the Thompson Sampling algorithm, which samples by estimating the posterior distribution, degraded. Estimates the distribution of parameters for the selected arm, taking advantage of the fact that the gram matrix $(X^TX)$ is block-diagonal when computing estimates due to the nature of the data. The inverse transform sampling method is used to sample parameters based on distributions, and the cholesky decomposition of the covariance matrix $\Sigma$ for the selected arm is used to improve sampling speed by storing the decomposed matrix separately.

### 4. Implement Algorithm
- We propose a LinUCB/LinTS-based weighted ordinal bandit (WO Bandit) with weights that reflect users' changing preferences.
- ![image](https://github.com/YeongHo-Lee/Weighted-Ordinal-Bandit-for-Streaming-Recommender-System/assets/77314467/304f9667-4627-44b3-8fe8-577f39074a3f)
- ![image](https://github.com/YeongHo-Lee/Weighted-Ordinal-Bandit-for-Streaming-Recommender-System/assets/77314467/db6f5ea1-378b-4288-b255-c7f9404146f7)

### 5. Result
- The two suggestion algorithms generated up to 7.7% more cumulative clicks than the rest of the existing algorithms.
- Performance is best when window size is small to give less consideration to recent positive news articles.
- ![image](https://github.com/YeongHo-Lee/Weighted-Ordinal-Bandit-for-Streaming-Recommender-System/assets/77314467/f4a01d94-8309-4568-91b1-6aff192228bf)

## Conclusion & Discussion
- Understand the LinUCB and LinTS algorithms, two of the most representative algorithms for CMAB problems using user information (context).
- Solve the problem of sampling degradation in the Thompson sampling algorithm as the dimensionality of the context vector increases.
-The absence of a theoretical analysis of the regret involved in the bandit algorithm.




