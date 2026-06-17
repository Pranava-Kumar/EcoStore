# ♻️ EcoStore: AI-Powered Green E-Commerce & Image Classifier

[![Framework: Flask](https://img.shields.io/badge/Framework-Flask-blue.svg)]()
[![Database: MongoDB](https://img.shields.io/badge/Database-MongoDB-green.svg)]()
[![CV Model: Keras/TensorFlow](https://img.shields.io/badge/CV-TensorFlow_Keras-orange.svg)]()
[![LLM: Qwen2.5-0.5B](https://img.shields.io/badge/LLM-Qwen2.5--0.5B-red.svg)]()

EcoStore is an intelligent green e-commerce platform that combines standard e-commerce features with on-device computer vision and a local LLM to promote recycling, reuse, and sustainable shopping.

---

## 📖 Architecture & AI Integration

EcoStore bridges web technology with artificial intelligence through a multi-model stack:

```
                  ┌──────────────────────┐
                  │   User Uploads Pic   │
                  └──────────┬───────────┘
                             │
                             ▼
                 ┌───────────────────────┐
                 │  Flask Web Controller │
                 └──────────┬────────────┘
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
    ┌───────────────────┐       ┌───────────────────┐
    │ Keras CNN Model   │       │ Qwen2.5-0.5B LLM  │
    │ (model_small.h5)  │       │ (Local Inference) │
    └─────────┬─────────┘       └─────────┬─────────┘
              │                           │
  [Classifies Image as]          [Generates Creative]
  ['organic' or 'recycle']       [Recycling Tutorials]
              │                           │
              ▼                           ▼
    ┌───────────────────┐       ┌───────────────────┐
    │ MongoDB Database  │       │ Rendered in UI    │
    │ (Auto-Categorize) │       │ (AI Chat view)    │
    └───────────────────┘       └───────────────────┘
```

---

## 🌟 Key Features

### 1. Computer Vision Product Classifier
- Implements a custom Convolutional Neural Network (CNN) trained in Keras (`organic_recycle_model.h5`) that runs local inference on product images.
- Images uploaded by merchants are resized to $80 	imes 45$ pixels, normalized, and classified into **`organic`** (biodegradable) or **`recycle`** (recyclable) categories.
- The product's database record is dynamically updated with the predicted category.

### 2. Local AI Recycling Assistant
- Integrates a locally run **`Qwen/Qwen2.5-0.5B`** causal language model using Hugging Face's `transformers` library and LangChain.
- Users input any object or household waste, and the local model generates a creative, 5-line upcycling guide, details whether it is biodegradable, and suggests the correct disposal method.
- By running a 0.5B parameter model locally, the app operates entirely free without external LLM API costs.

### 3. Core E-Commerce Features
- MongoDB database integration (`pymongo`) storing users, products, purchases, and community posts.
- User authentication with `flask_bcrypt` password hashing.
- Interactive community section where users share upcycled creations and recycling wins.

---

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.10+
- MongoDB instance running locally on `mongodb://localhost:27017`
- NVIDIA GPU or CPU (the 0.5B LLM runs comfortably on CPU)

### Setup Instructions
1. Install dependencies:
   ```bash
   pip install Flask flask_bcrypt pymongo tensorflow Pillow transformers torch langchain-community
   ```
2. Start MongoDB:
   ```bash
   mongod --dbpath /path/to/your/db
   ```
3. Run the Flask web app:
   ```bash
   python app.py
   ```
4. Access the web app at `http://localhost:5000`.
