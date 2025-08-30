# CSV Cleaner

A lightweight Python utility to quickly clean CSV files by removing **duplicate rows** and **blank rows**, then saving the cleaned data into a new CSV file.  

## ✨ Features
- Removes all **duplicate rows** from your CSV.  
- Strips out any **blank/empty rows**.  
- Saves the cleaned file separately so the original data stays intact.  
- Fast and simple to use — works with any standard CSV file.  

## 🚀 How It Works
1. User provides the input CSV file.  
2. The program reads the data and removes duplicates + blanks.  
3. The cleaned CSV is saved into a new file (e.g., `cleaned_data.csv`).  

## 📦 Requirements
- Python 3.x  
- `pandas` library  

Install dependencies with:
```bash
    pip install pandas
