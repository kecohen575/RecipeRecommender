# Next Steps: Recipe Recommender Project

## What We've Done So Far ✅

**Good news**: We've completed the hardest part - understanding our data!

1. ✅ **Data loaded**: We have 700K training examples (more than enough!)
2. ✅ **Exploratory analysis done**: We understand the data patterns
   - Ratings are mostly 4-5 stars (people rate things they like)
   - Most users rate <10 recipes (sparse data)
   - Most recipes have few ratings (cold-start problem)
   - 99.8% sparsity (normal for recommendation systems)
3. ✅ **Documentation**: README and analysis documents created

## What We Need To Do Now 🎯

We need to build **recommendation models** and **evaluate** them. Here's the plan:

---

## Phase 1: Build Simple Baselines (2-3 days) ⚠️ START HERE

**Why**: We need simple models to compare against. These are easy to build and show we understand the basics.

### Task 1.1: Popularity Recommender
**What**: Recommend recipes that everyone likes (most rated)
**How**: Count how many times each recipe was rated, recommend top 10
**Who can do**: Anyone (easiest one)

### Task 1.2: User Mean Predictor  
**What**: Predict a user will like recipes similar to their average rating
**How**: Calculate each user's average rating, use that to predict
**Who can do**: Anyone (simple math)

### Task 1.3: Item Mean Predictor
**What**: Predict based on how good the recipe usually is
**How**: Calculate each recipe's average rating, use that to predict
**Who can do**: Anyone (simple math)

**Deliverable**: Three working baseline models that can make predictions

---

## Phase 2: Build Advanced Model (3-4 days) ⚠️ CRITICAL

**Why**: This is the main model that should beat the baselines. Required for assignment.

### Task 2.1: Matrix Factorization Model
**What**: Learn hidden patterns in user-recipe interactions
**How**: 
- Option A: Use `scikit-surprise` library (easier, faster)
- Option B: Implement from scratch (more educational)
**Who can do**: Someone comfortable with ML/math

**What it does**: 
- Learns "user preferences" (e.g., likes spicy food, vegetarian)
- Learns "recipe features" (e.g., spicy, vegetarian, quick)
- Predicts ratings by matching preferences to features

**Deliverable**: One working matrix factorization model

---

## Phase 3: Build Evaluation System (2-3 days) ⚠️ CRITICAL

**Why**: We need to measure how good our models are. Required for assignment.

### Task 3.1: Ranking Metrics
**What**: Measure how well models rank recipes (not just predict ratings)
**Metrics to implement**:
- Precision@K: Of top K recommendations, how many did user actually like?
- Recall@K: Of recipes user liked, how many did we recommend?
- MRR: How high in the list is the first correct recommendation?
- NDCG: How good is the ranking order?

**Who can do**: Anyone (standard formulas, can look up implementations)

### Task 3.2: Evaluation Protocol
**What**: Test models on validation/test set
**How**: 
1. For each user in test set
2. Generate top 10 recipe recommendations
3. Check if those recipes match what user actually rated highly
4. Calculate metrics

**Deliverable**: Evaluation code that produces comparison table (baselines vs. advanced model)

---

## Phase 4: Content Features (Optional, 2-3 days) 📝 IF TIME PERMITS

**Why**: Helps with cold-start problem (recipes with few ratings)

### Task 4.1: Recipe Difficulty Features
**What**: Extract features from recipe metadata
**Features**:
- Instruction length (longer = harder)
- Number of ingredients (more = harder)
- Ingredient rarity (rare = harder)
- Estimated cooking time

**Who can do**: Anyone comfortable with data processing

**Deliverable**: Feature extraction code (can add to model later)

---

## Phase 5: Related Work & Presentation (2-3 days) ⚠️ CRITICAL

### Task 5.1: Literature Review
**What**: Find papers that used Food.com dataset or similar approaches
**How**: Google Scholar search for "Food.com recommendation" or "recipe recommendation"
**Who can do**: Anyone (research task)

### Task 5.2: Presentation Prep
**What**: Create ~20 minute video presentation
**Content**:
- Slides explaining our approach
- Code walkthrough
- Results comparison
**Who can do**: Team effort

**Deliverable**: Video + HTML notebook export

---

## Timeline Summary

| Phase | Task | Days | Priority | Status |
|-------|------|------|----------|--------|
| 1 | Baselines | 2-3 | HIGH | ⚠️ TODO |
| 2 | Matrix Factorization | 3-4 | HIGH | ⚠️ TODO |
| 3 | Evaluation | 2-3 | HIGH | ⚠️ TODO |
| 4 | Content Features | 2-3 | MEDIUM | ⚠️ OPTIONAL |
| 5 | Related Work & Presentation | 2-3 | HIGH | ⚠️ TODO |

**Total**: ~12-16 days of focused work

---

## Assignment Requirements Checklist

The assignment needs 5 sections (5 marks each):

1. ✅ **Predictive Task**: Define what we're doing (mostly done, need to formalize)
2. ✅ **Exploratory Analysis**: DONE! (Section 2 complete)
3. ⚠️ **Modeling**: Need to implement (Phase 1 + 2)
4. ⚠️ **Evaluation**: Need to implement (Phase 3)
5. ⚠️ **Related Work**: Need to research (Phase 5)

---

## Simple Explanation for Teammates

**What we're building**: A system that recommends recipes to users based on their past ratings.

**How it works**:
1. **Baselines** (simple): "Recommend popular recipes" or "Recommend recipes similar to user's average"
2. **Advanced model** (smart): Learns patterns like "users who like spicy food also like these recipes"
3. **Evaluation**: Test how good our recommendations are

**Why we're doing this**: 
- Assignment requires it
- Shows we understand recommendation systems
- Baselines prove our advanced model is better

**What we need**:
- Someone to build baselines (easy, good starting point)
- Someone to build matrix factorization (harder, main model)
- Someone to build evaluation (medium, required)
- Everyone to help with presentation

---

## Questions to Discuss

1. **Who wants to work on what?**
   - Baselines (easiest, good for learning)
   - Matrix Factorization (harder, main model)
   - Evaluation (medium, required)
   - Related Work (research, can do anytime)

2. **Library choice**: Use `scikit-surprise` (easier) or implement from scratch (more educational)?

3. **Timeline**: When is the assignment due? How much time do we have?

4. **Division of work**: Should we split tasks or pair program?

---

## Resources

- **scikit-surprise**: https://surpriselib.com/ (recommendation library)
- **Matrix Factorization tutorial**: Can find online tutorials
- **Ranking metrics**: Standard formulas, can look up
- **Food.com papers**: Search Google Scholar

---

## Bottom Line

**We're in good shape!** The data analysis is done. Now we need to:
1. Build 3 simple baselines (2-3 days)
2. Build 1 advanced model (3-4 days)  
3. Build evaluation system (2-3 days)
4. Research related work (2-3 days)
5. Make presentation (2-3 days)

**Total: ~2 weeks of work**. We can do this! 🚀

