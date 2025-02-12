# 🥗 Vegetarian Recipe Recommendation Chatbot  

## 📌 Overview  
This project is an **AI-powered recipe recommendation chatbot** that suggests vegetarian dishes based on the user's available ingredients. It provides:  
- **Customized Recipe Suggestions** 🥘  
- **Step-by-Step Cooking Instructions** 👨‍🍳  
- **Nutritional Information (Calories, Protein, etc.)** 🍎  

The system utilizes **Large Language Models (LLMs)** for natural language understanding and **vector-based retrieval** for recipe matching. It is designed to be interactive and user-friendly, making vegetarian cooking accessible to everyone.  

## 🎯 Key Features  
✅ **Ingredient-Based Recipe Recommendations**: Users provide ingredients they have, and the chatbot suggests suitable vegetarian recipes.  
✅ **Nutritional Insights**: Retrieves macronutrient details (calories, protein, carbs, etc.) using **USDA macronutrient data**.  
✅ **Step-by-Step Cooking Instructions**: Uses LLM-generated or dataset-based structured instructions for ease of cooking.  
✅ **Fast & Efficient Retrieval**: Uses **LLaMA embeddings & ChromaDB** for optimized recipe searches.  

## 📂 Dataset  
The dataset is sourced from **Food.com**, containing over **10,000+ vegetarian recipes** with:  
- **Ingredients List**  
- **Cooking Instructions**  
- **Nutritional Information** (calories, protein, fats, etc.)  
- **User Ratings & Reviews**  

## 🛠️ Tech Stack  
🔹 **Natural Language Processing (NLP)**: LLaMA embeddings for ingredient similarity & retrieval  
🔹 **Vector Database**: ChromaDB for fast recipe search  
🔹 **Language Model Integration**: OpenAI API for chatbot conversation & recipe generation  
🔹 **Data Processing**: Python (Pandas, NumPy) for cleaning and feature engineering  
🔹 **Web Interface (Optional)**: Streamlit-based UI for chatbot interactions  

📽️ [Watch the demo video](video/demo.mov)
