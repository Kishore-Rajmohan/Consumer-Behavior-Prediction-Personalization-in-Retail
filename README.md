# 🛍️ Consumer Behavior Prediction and Personalization in Retail

---

## 🎯 What This Project Is About

Retail businesses collect a lot of customer data but most of them
don't really know what to do with it. They send the same email to
everyone, stock products based on gut feeling, and only find out
about fraud after the damage is done.

I wanted to see if machine learning could actually fix that not
in theory, but with real data. So I took a dataset of 3,900 retail
customers and built a pipeline that answers three questions:

- 👥 Who are my customers and how do I group them?
- 🚨 Is anything suspicious happening in my transactions?
- 🔮 What will my customers buy next?

---

## 💼 The Business Problem

Imagine you run an online clothing store. You've got thousands of
customers but you're treating them all the same promotions,
same emails, same everything. Some of them haven't bought anything
in months. Some of them spend hundreds every week. You're wasting
money on people who don't care and not rewarding the ones who do.

On top of that, you have no idea if some of those transactions are
fraudulent until it's too late.

This project tackles all of that.

---

## 🛠️ Skills & Tools

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat&logo=keras&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-189AB4?style=flat)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

**What I applied:**
- 🔵 Unsupervised Learning (DBSCAN, Autoencoders)
- 🟢 Deep Learning (TCN, GRU, LSTM)
- 📈 Time-Series Forecasting
- 🔴 Anomaly Detection
- ⚙️ Feature Engineering
- 📊 Data Visualisation (t-SNE, heatmaps, error distributions)

---

## 🔍 What I Did

I didn't just train one model and call it done. I built three
separate systems that work together:

**👥 Customer Segmentation**
Used DBSCAN to group customers by how often they buy and how much
they spend. Ended up with 113 clusters and flagged 1,344 outliers
that needed a closer look.

**🚨 Anomaly Detection**
Trained an Autoencoder to learn what "normal" purchasing looks like,
then flagged anything that didn't fit. About 5% of the data came
back as anomalous some of those are probably fraud, some are just
unusual high value customers worth paying attention to.

**🔮 Purchase Forecasting**
Compared six different models TCN, GRU, LSTM, XGBoost, Attention,
and a Hybrid GRU Attention modelto see which one predicted future
purchases most accurately.

---

## 📊 Exploratory Data Analysis

Before building anything I spent time just understanding the data.

**What categories do people buy?**

![Product Category Distribution](Images/Product%20Category%20Distribution.png)

Clothing is by far the most purchased category, nearly double
Accessories. Outerwear barely features — useful to know for
stock planning.

**Does gender affect what people buy?**

![Heatmap of Product Categories by Gender](Images/Heatmap%20of%20Product%20Categories%20by%20Gender.png)

Males buy significantly more Clothing (1,181 vs 556) and
Accessories (848 vs 392). That's not a small gap — it has real
implications for who you target with what campaigns.

---

## 👥 Clustering Results

![DBSCAN Clustering Results](Images/DBSCAN%20Clustering%20Results.png)

The t-SNE plot shows the customer clusters. Most customers sit in
that dense purple mass in the middle — your typical average shoppers.
The scattered coloured dots are the interesting ones — niche segments
that behave differently and probably need a different approach.

| 📌 What We Found | Number |
|---|---|
| Clusters Identified | 113 |
| Outliers Flagged | 1,344 |
| Silhouette Score | -0.372 |
| Davies Bouldin Index | 1.634 |

Honest note — the Silhouette Score being negative tells you the
clusters overlap quite a bit. That's partly a limitation of the
dataset and partly something I'd tune further with more time.

---

## 🚨 Anomaly Detection

![Reconstruction Errors from Autoencoder](Images/Reconstruction%20Errors%20from%20Autoencoder.png)

The dashed line is the 95th percentile threshold. Anything to the
right of that got flagged. Most transactions are normal and sit
in that bell curve. The ones that fall way outside it are worth
a second look — could be fraud, could be a bulk buyer, could be
a data error.

| 📌 What We Found | Number |
|---|---|
| Anomalies Detected | 195 |
| Percentage of Data | ~5% |

---

## 🤖 Model Performance

I trained and compared six models. Here's how they did:

| Model | MAE | RMSE |
|---|---|---|
| ⭐ TCN (Best) | 12.02 | — |
| GRU | 12.03 | 14.17 |
| LSTM | 12.04 | — |
| Attention | 12.07 | 14.19 |
| Hybrid GRU Attention | 12.12 | 14.26 |
| XGBoost | 12.45 | — |

TCN came out on top but honestly the differences are small. What
matters more is picking the right model for the right job — TCN
for sequential forecasting, GRU if you need speed, XGBoost if
you want to explain your predictions to a non technical team.

**📉 GRU Training & Validation Loss**

![GRU Model](Images/GRU.png)

**📉 TCN Training & Validation Loss**

![TCN Model Evaluation](Images/TCN%20Model%20Evaluation.png)

Both models learned quickly and didn't overfit — the training
and validation loss lines stay close together after the first
few epochs which is exactly what you want to see.

**🔑 What actually drives customer behaviour?**

![XGBoost Feature Importance](Images/XGBoost%20Feature%20Importance.png)

The Purchase_Review_Interaction feature I engineered turned out
to be the most important predictor (~0.44). That's the relationship
between how much someone spends and how satisfied they are —
turns out that combination tells you a lot about what they'll
do next.

---

## 💡 What This Means for a Real Business

Based on what I found, here's what I'd actually recommend:

**👥 On segmentation** — stop treating all customers the same.
Your high spend frequent buyers deserve a loyalty programme.
Your one time buyers need a reengagement campaign, not the
same newsletter as everyone else.

**🚨 On anomaly detection** — automate the flagging. You don't
need someone manually reviewing every transaction. Build a
threshold, flag what's above it, let the fraud team handle
the rest.

**🔮 On forecasting** — use the TCN for seasonal planning.
If you know a spike is coming you can actually prepare for
it rather than scrambling when stock runs out.

---

## 🔭 What I'd Do Differently / Next Steps

This project has limitations and I want to be upfront about them:

- The dataset is structured only — no customer reviews, no
  social media data, no browsing behaviour. That stuff would
  make the models significantly better
- The clustering quality wasn't perfect — I'd spend more time
  tuning DBSCAN parameters or try a different algorithm entirely
- Everything here is offline — a real system would need to
  process data in real time
- Needs testing on bigger, more varied datasets before anyone
  deploys this in production

Things I'd build next:
- [ ] 🔴 Real time fraud flagging pipeline
- [ ] 💬 Sentiment analysis on customer reviews
- [ ] 🌐 REST API to serve the TCN predictions live
- [ ] 🔍 Explainability layer so non technical stakeholders
        can trust the outputs

---

## 📁 Files in This Repo

```
├── 🖼️ Images/
│   ├── DBSCAN Clustering Results.png
│   ├── GRU.png
│   ├── Heatmap of Product Categories by Gender.png
│   ├── Product Category Distribution.png
│   ├── Reconstruction Errors from Autoencoder.png
│   ├── TCN Model Evaluation.png
│   └── XGBoost Feature Importance.png
├── 📓 Consumer_Behavior_Prediction_and_Personalization_in_Retail.ipynb
├── 📄 ConsumerBehaviour.pdf
├── 📊 shopping_trends.csv
└── 📝 README.md
```

---
