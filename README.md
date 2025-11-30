# 4-Week Intensive Social Feed Recommendation Algorithms Learning Program

> [!NOTE]
> This curriculum is written by Claude.

> **Total Time Commitment**: 80-100 hours (20-25 hours/week)

---

## Week 1: Foundations + Twitter's Architecture

### Goals

- Understand basic recommender system concepts
- Learn how production social feed algorithms work
- Get familiar with evaluation metrics

### Reading (10-12 hours)

**1. Mining of Massive Datasets - Chapter 9 (Focus: Sections 9.1-9.4)**

- Link: http://www.mmds.org/
- Topics: Collaborative filtering, content-based filtering, evaluation metrics
- Pages 307-330 (skim 331-346)

**2. Twitter's Recommendation Algorithm** ⭐ CRITICAL

- Blog post: https://blog.x.com/engineering/en_us/topics/open-source/2023/twitter-recommendation-algorithm
- Read thoroughly, take detailed notes on:
  - Three-stage pipeline (candidate sourcing → ranking → filtering)
  - In-network vs. out-of-network sources
  - SimClusters embedding approach

**3. Twitter Algorithm Overview**

- InfoQ summary: https://www.infoq.com/news/2023/04/twitter-algorithm/
- Provides good diagrams and explanations

**4. Twitter's Open Source Code (Browse only)**

- Main repo: https://github.com/twitter/the-algorithm
- ML models: https://github.com/twitter/the-algorithm-ml
- Just understand the structure, don't read all code

### Hands-on Project (10-13 hours)

**Mini-Project: Build Basic Recommender**

1. Download MovieLens 100K dataset
   - Link: https://grouplens.org/datasets/movielens/100k/
2. Implement user-user collaborative filtering
   - "Users who agreed in the past will agree in the future"
   - Find users similar to you
   - Recommend items those similar users liked
3. Calculate metrics: Precision@10, Recall@10, NDCG
4. Compare with item-item collaborative filtering
   - "Items similar to what you liked, you'll probably like too"
   - Find items similar to items you've liked
   - Recommend those similar items

**Tools needed:**

- Python, pandas, numpy, scikit-learn

### Deliverables

- [ ] Working collaborative filtering implementation
- [ ] Twitter architecture diagram (draw it yourself)
- [ ] List of 15+ ranking signals Twitter uses
- [ ] Evaluation metrics comparison table

---

## Week 2: Deep Learning Architecture + Reddit Data

### Goals

- Master two-stage neural ranking architecture
- Work with real social media data
- Implement candidate generation + ranking

### Reading (8-10 hours)

**1. "Deep Neural Networks for YouTube Recommendations" (2016)** ⭐⭐ MOST IMPORTANT

- Paper: https://research.google/pubs/deep-neural-networks-for-youtube-recommendations/
- ACM version: https://dl.acm.org/doi/10.1145/2959100.2959190
- Read 2-3 times, focus on:
  - Two-stage architecture
  - Candidate generation as extreme multiclass classification
  - Ranking with neural network
  - Feature engineering tricks

**2. YouTube Paper Analysis (helpful supplement)**

- Summary: https://shagunsodhani.com/papers-I-read/Deep-Neural-Networks-for-YouTube-Recommendations
- Practical guide: https://happystrongcoder.substack.com/p/deep-neural-networks-for-youtube

**3. Reddit Dataset Documentation**

- Pushshift paper: https://ojs.aaai.org/index.php/ICWSM/article/download/7347/7201
- Parsing guide: https://medium.com/@MaLiN2223/getting-data-from-pushshift-archives-b3bc0e487359

### Hands-on Project (12-15 hours)

**Major Project: Two-Stage System with Reddit Data**

**Step 1: Get Reddit Data (3-4 hours)**

1. Download 2-3 subreddits from Academic Torrents
   - Top 40k subreddits: https://academictorrents.com/details/1614740ac8c94505e4ecb9d88be8bed7b6afddd4
   - Choose small ones: r/movies, r/technology (1 month only)
2. Use parsing scripts: https://github.com/Watchful1/PushshiftDumps
3. Extract: posts, comments, scores, authors, timestamps

**Step 2: Build Two-Stage System (9-11 hours)**

**Stage 1 - Candidate Generation:**

- In-network: Posts from "followed" users (simulate with top posters)
- Out-of-network: Popular posts by score
- Reduce from 10,000s posts to ~100-200 candidates

**Stage 2 - Ranking:**

- Features: recency, score, comment_count, author_karma
- Model: Logistic regression predicting "will user upvote?"
- Output: Ranked feed

### Deliverables

- [ ] Parsed Reddit dataset (2-3 subreddits, 1 month)
- [ ] Working two-stage ranking system
- [ ] Comparison: chronological vs. ranked feed
- [ ] Code on GitHub

---

## Week 3: Advanced Ranking + Multi-Objective Optimization

### Goals

- Implement production-quality features
- Learn multi-objective optimization
- Understand algorithmic effects

### Reading (6-8 hours)

**1. Algorithm Effects Research**

- "Understanding Social Media Recommendation Algorithms"
  - Link: https://knightcolumbia.org/content/understanding-social-media-recommendation-algorithms
  - Focus on engagement prediction and demotion

**2. Recent Research (skim abstracts, read key sections)**

- Engagement vs. satisfaction: https://academic.oup.com/pnasnexus/article/4/3/pgaf062/8052060
- Feed reranking guide: https://arxiv.org/html/2406.19571v1

**3. Value Alignment Paper (optional but interesting)**

- Link: https://arxiv.org/html/2509.14434v1

### Major Project (14-17 hours)

**Build Production-Quality Feed Ranker**

**Part 1: Advanced Features (6-8 hours)**
Add to your Week 2 system:

- **Embeddings**: Use word2vec or simple averaging for content similarity
- **Engagement velocity**: Score/time since posted
- **Author credibility**: Historical average score
- **Diversity features**: Topic variety (use keywords)
- **Freshness decay**: Time-based penalty

**Part 2: Multi-Objective Ranking (5-6 hours)**
Optimize for multiple goals:

1. **Engagement**: Predicted clicks/upvotes
2. **Diversity**: Different authors, topics
3. **Quality**: Filter clickbait (titles with "!!" or all caps)

Implement:

- Weighted scoring: `final_score = 0.6*engagement + 0.3*quality + 0.1*diversity`
- Re-ranking for diversity (ensure not all from one author)

**Part 3: Evaluation (3 hours)**
Compare three approaches:

1. Chronological (baseline)
2. Engagement-only ranking
3. Multi-objective ranking

Metrics:

- Engagement: CTR simulation, average score
- Diversity: Unique authors in top 20, topic coverage
- Quality: Average length, reduced clickbait

### Deliverables

- [ ] Enhanced ranking system with embeddings
- [ ] Multi-objective optimization implementation
- [ ] Evaluation report comparing 3 approaches
- [ ] Visualizations (graphs showing improvements)

---

## Week 4: Final Project + Portfolio

### Goals

- Create production-quality demonstration
- Build portfolio piece
- Synthesize all learning

### Minimal Reading (2-3 hours)

**Review and Consolidate:**

- Re-read Twitter blog post
- Re-skim YouTube paper key sections
- Review your own notes and code

**Optional: Latest Trends**

- Browse RecSys conference: https://recsys.acm.org/
- Check recent papers on arXiv (just abstracts)

### Final Project (18-22 hours)

**Build: Complete Feed Ranking System Demo**

**Requirements:**

**1. Data Pipeline (3-4 hours)**

- Load and process Reddit data efficiently
- Create user simulation (which users to show feed to)
- Split into train/test sets

**2. Complete Ranking System (6-8 hours)**
Implement all stages:

- **Candidate Generation**:
  - In-network source
  - Out-of-network via embeddings/popularity
  - Return ~150 candidates
- **Ranking**:
  - Neural network or gradient boosted trees
  - Features from Week 3
  - Predict engagement probability
- **Filtering**:
  - Remove seen posts
  - Ensure diversity (max 2 from same author in top 10)
  - Apply content filters

**3. Evaluation Framework (3-4 hours)**

- Offline metrics: Precision@K, NDCG, diversity
- Simulate user behavior (click top-K posts)
- Compare against baselines

**4. Documentation + Visualization (4-5 hours)**
Create README with:

- Architecture diagram
- Feature engineering explanation
- Results with graphs
- Example outputs (sample feeds)
- How to run the code

**5. Polish (2-3 hours)**

- Clean up code
- Add comments
- Create requirements.txt
- Write usage examples

### Deliverables

- [ ] Complete GitHub repository
- [ ] README with architecture and results
- [ ] Working demo (command-line is fine)
- [ ] Evaluation report with visualizations
- [ ] (Optional) Simple web UI using Flask/Streamlit

---

## Essential Resources Quick Reference

### Datasets

- **MovieLens 100K**: https://grouplens.org/datasets/movielens/100k/
- **Reddit (Academic Torrents)**: https://academictorrents.com/details/1614740ac8c94505e4ecb9d88be8bed7b6afddd4
- **Parsing Scripts**: https://github.com/Watchful1/PushshiftDumps

### Must-Read Papers

1. **YouTube (2016)**: https://research.google/pubs/deep-neural-networks-for-youtube-recommendations/
2. **Twitter (2023)**: https://blog.x.com/engineering/en_us/topics/open-source/2023/twitter-recommendation-algorithm
3. **Mining Massive Datasets**: http://www.mmds.org/

### Code & Tools

- **Twitter's Algorithm**: https://github.com/twitter/the-algorithm
- **Python Libraries**: pandas, numpy, scikit-learn, pytorch/tensorflow
- **Embeddings**: gensim (word2vec), sentence-transformers
- **Similarity Search**: FAISS (optional, for scale)

### Supplementary Resources

- **RecSys Conference**: https://recsys.acm.org/
- **Stanford CS246**: http://web.stanford.edu/class/cs246/
- **UCSD RecSys Data**: https://cseweb.ucsd.edu/~jmcauley/datasets.html

---

## Weekly Time Breakdown

### Week 1: 20-25 hours

- Reading: 10-12 hours
- Coding: 10-13 hours

### Week 2: 20-25 hours

- Reading: 8-10 hours
- Coding: 12-15 hours

### Week 3: 20-25 hours

- Reading: 6-8 hours
- Coding: 14-17 hours

### Week 4: 20-25 hours

- Reading: 2-3 hours
- Final project: 18-22 hours

**Total: 80-100 hours over 4 weeks**

---

## Study Tips

### Maximize Learning Efficiency

1. ✅ **Read with purpose** - Take notes, highlight key algorithms
2. ✅ **Code immediately** - Don't wait to implement concepts
3. ✅ **Start simple** - Get basic version working first
4. ✅ **Compare approaches** - Always benchmark against baselines
5. ✅ **Document as you go** - Write README sections while coding

### Common Pitfalls to Avoid

- ❌ Downloading entire Reddit dataset (TB+) → Use 1-3 subreddits, 1 month
- ❌ Perfect code before testing → Get it working, then improve
- ❌ No evaluation metrics → You can't improve what you don't measure
- ❌ Reading without implementing → Knowledge fades fast
- ❌ Skipping YouTube paper → It's the foundation

### When You Get Stuck

1. Re-read the relevant paper section
2. Check Twitter's open source code for examples
3. Start with simpler version (smaller data, fewer features)
4. Ask on Reddit: r/MachineLearning, r/learnmachinelearning
5. Review your Week 1 basics

---

## Expected Outcomes

After 4 weeks, you will:

- ✅ Understand how Twitter and YouTube recommendation systems work
- ✅ Have built a complete two-stage ranking system
- ✅ Know key algorithms: collaborative filtering, embeddings, neural ranking
- ✅ Have experience with real social media data (Reddit)
- ✅ Own a portfolio project demonstrating RecSys skills
- ✅ Be ready for RecSys roles or further research

---

## Next Steps After Completion

### Immediate (Week 5)

1. **Polish portfolio**: Clean code, better documentation, add visualizations
2. **Write blog post**: Explain what you built and learned
3. **Share on LinkedIn/Twitter**: Tag relevant people, show your work

### Short-term (Months 2-3)

1. **Apply to jobs**: Look for ML/RecSys engineer positions
2. **Contribute to open source**: Twitter algorithm, other RecSys projects
3. **Take RecSys Challenge**: Annual competition (when available)
4. **Deep dive**: Pick one area (embeddings, multi-objective, etc.) to master

### Long-term (Months 4+)

1. **Read latest papers**: Follow RecSys, KDD, WWW conferences
2. **Build production system**: Deploy your ranker as web app
3. **Specialize**: Choose focus (e.g., cold start, diversity, real-time systems)
4. **Teach others**: Write tutorials, make YouTube videos

---

## Success Metrics

Track your progress:

- [ ] Week 1: Basic collaborative filtering working
- [ ] Week 2: Two-stage system with Reddit data
- [ ] Week 3: Multi-objective ranking implemented
- [ ] Week 4: Portfolio project on GitHub
- [ ] Bonus: Blog post written and shared

---

## Additional Notes

### Hardware Requirements

- **Minimum**: Laptop with 8GB RAM, any modern CPU
- **Recommended**: 16GB RAM, GPU helpful but not required
- **Dataset size**: Start with <5GB of Reddit data

### Software Requirements

```bash
# Python 3.8+
pip install pandas numpy scikit-learn
pip install torch  # or tensorflow
pip install matplotlib seaborn  # for visualizations
pip install jupyter  # for notebooks
pip install gensim  # for embeddings
```

### Time Management Strategy

- **Daily**: 3-4 hours if doing weekdays only
- **Weekends**: 6-8 hours for major projects
- **Ideal**: 2 hours reading + 2-3 hours coding daily

---

## Contact & Community

### Get Help

- **Reddit**: r/MachineLearning, r/learnmachinelearning
- **Stack Overflow**: Tag with [recommender-system]
- **GitHub Discussions**: On Twitter's algorithm repo

### Stay Updated

- **Twitter**: Follow @karpathy, @ylecun, RecSys researchers
- **ArXiv**: Search "recommendation systems" weekly
- **Blogs**: Netflix Tech Blog, Meta AI Research

---

## Final Checklist

Before starting:

- [ ] Time commitment confirmed (20-25 hrs/week)
- [ ] Python environment set up
- [ ] GitHub account ready
- [ ] Downloaded Mining Massive Datasets book
- [ ] Bookmarked all key links

After Week 4:

- [ ] GitHub repo with complete code
- [ ] README with results and visualizations
- [ ] Working demo
- [ ] Blog post or LinkedIn write-up
- [ ] Applied learnings to resume/portfolio

---

**Good luck! Start with Week 1 and build consistently. You've got this! 🚀**

---

_Last updated: November 2025_
_For questions or suggestions: Create an issue on your GitHub project_
