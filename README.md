#### 📌 Project Overview

This project is an LLM-powered Exploratory Data Analysis (EDA) tool that allows users to upload a CSV file and automatically generate insights, data summaries, and visualizations. It leverages Gradio for an interactive UI and Mistral-7B (via Ollama) for AI-powered analysis.

##### 🔍 Code Breakdown

**1. Importing Libraries**

import gradio as gr

import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns

import ollama

- Gradio: Used to create the interactive web interface.
- Pandas: Handles CSV data processing.
- Matplotlib & Seaborn: Generate visualizations.
- Ollama: Enables AI-powered insights using Mistral-7B.


**2. Function: eda_analysis(file_path)**

This function processes the uploaded CSV file and performs:

**Missing value handling:**

- Numeric columns → Filled with median

- Categorical columns → Filled with mode

**Data Summary:**

- Generates df.describe(include='all')

- Identifies missing values

**AI-Powered Insights:**

- Calls generate_ai_insights() for LLM-generated analysis

**Visualizations:**

- Calls generate_visualizations() to create plots
  
- Returns the processed report and generated plots

- 
**3. Function: generate_ai_insights(df_summary)**

def generate_ai_insights(df_summary):
    prompt = f"Analyze the dataset summary and provide insights:\n\n{df_summary}"
    response = ollama.chat(model="mistral", messages=[{"role": "user", "content": prompt}])
    return response['message']['content']
    
- Constructs a prompt using the dataset summary.

- Sends the prompt to Mistral-7B via Ollama.

- Returns AI-generated insights.


**4. Function: generate_visualizations(df)**
Creates histograms for numeric columns and a correlation heatmap.

python
Copy
Edit
plt.savefig(path)  # Saves each plot as an image
plot_paths.append(path)  # Stores the paths for Gradio to display
Histograms show data distributions.
Heatmap visualizes feature correlations.
5. Gradio Interface
python
Copy
Edit
demo = gr.Interface(
    fn=eda_analysis,
    inputs=gr.File(type="filepath"),
    outputs=[gr.Textbox(label="EDA Report"), gr.Gallery(label="Data Visualizations")],
    title="📊 LLM-Powered Exploratory Data Analysis (EDA)",
    description="Upload any dataset CSV file and get automated EDA insights with AI-powered analysis and visualizations."
)
Uses Gradio to create a web-based UI.
Allows users to upload a CSV file.
Outputs text-based insights and visualizations.
6. Running the Application
python
Copy
Edit
demo.launch(share=True)
Launches the app with Gradio.
Enables public sharing of the interface.
📥 Installation & Usage
1️⃣ Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/LLM-Powered-EDA.git
cd LLM-Powered-EDA
2️⃣ Install Dependencies
bash
Copy
Edit
pip install gradio pandas matplotlib seaborn ollama
3️⃣ Start Ollama & Pull Mistral Model
bash
Copy
Edit
ollama pull mistral:latest
4️⃣ Run the Application
bash
Copy
Edit
python app.py
Opens a Gradio interface in the browser.
Upload a CSV file and get automated EDA insights.
🌟 Why Use This Project?
✔ No Manual EDA – Fully automated insights
✔ AI-Powered Analysis – Uses LLM for intelligent insights
✔ Visualizations – Understand data distributions easily
✔ User-Friendly UI – No coding required
