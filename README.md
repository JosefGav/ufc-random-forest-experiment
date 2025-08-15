# 🥊 UFC Fight Outcome Prediction (Exploratory Project)

This project explores a dataset containing UFC fight records from [Kaggle](https://www.kaggle.com/datasets/rajeevw/ufcdata).  
The goal is to **predict fight outcomes** based on a fighter’s past performance using machine learning.

This project was completed with a larger project in mind - involving scraping and manipulating my own data. 
This serves as a practice run using already collected and cleaned data, helping me better understand the model training that i will be doing in my next project

---

## 📌 Key Highlights

- Used a **Random Forest** classifier to predict the winner based on pre-fight statistics.
- Achieved an initial test **accuracy of 67.7%** using a model saved as `mma_model.pkl`.
- Identified **bias** in the dataset favoring the "red" fighter (who wins 67.4% of the time).
- Ran multiple experiments to test how this bias affects model performance.

---

## 📊 Data Bias Observation

In the dataset, fighters are labeled as either **red** or **blue**.  
While these labels are arbitrary (in the same way that the color of shorts a fighter wears is arbitrary), the **red fighter won 67.4%** of the time.

> This means that simply predicting “red” for every match gives a baseline accuracy of ~67.4%, similar to the model.

### 🔁 Confusion Matrix (Original Dataset):
    Predicted
         B     R
      -------------
B |    39   346   <- Actual Loss
R |    36   760   <- Actual Victory

- The model **rarely predicted "blue"**, but when it did, it was **correct nearly 50%** of the time.
- This suggests potential for combining model predictions with **betting odds** — betting only on the underdog when the model shows strong confidence.
- This opens the door to various betting strategies (e.g., wager only when the model confidently predicts an underdog win — a rare event, but potentially profitable).


---

## 🧪 Experiment: Useless Features

I removed meaningful features and used only the least informative one — **number of draws** — which has nearly zero correlation with fight outcome as they are an extremely rare occurance.

> Surprisingly, the model still reached 67.4% accuracy by **predicting "red" every time**.

### Confusion Matrix (Useless Features):
    B   R
 [[  0 385] <- loss
 [  0 796]] <- victory

This confirms the **strong class imbalance**: the model learns to always guess "red" to maximize accuracy.

---

## ⚖️ Fixing the Class Imbalance

To test further, I balanced the dataset to have an equal 50/50 split between red and blue winners.  
This quick fix (for testing only) yielded a more meaningful result.

- ✅ **Accuracy dropped to 58.3%** on unseen data — a more realistic performance baseline.
- Given the unpredictable nature of UFC fights, this result is still promising.

---

## 🔄 Next Steps

- Scrape or collect **more recent fight data** (post-2021).
- Improve **feature engineering** (e.g., more features, include betting odds, round specific stats, differenciate between recent and historical fight performance).
- Explore **ensemble methods** to improve predictive power.

---

## 📁 Files

- `mma_model.pkl` – Trained Random Forest model
- `fair_model.pkl` – Random Forest model trained on less biased data
- `output.png` – Feature importance chart
- `notebooks/` – Jupyter notebooks with EDA and model training
- `requirements.txt` – List of dependencies

---

## 💡 Final Thoughts

This started as a curiosity-driven experiment and turned into a deeper look at bias in datasets.  
It also revealed that even a "dumb" model can appear smart when data is skewed — a valuable lesson in data science.
