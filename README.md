
# **Hotel Booking Data Processing & RAG-Based Q&A System**  

## **Overview**  
This project processes **hotel booking data**, extracts key insights, and enables **Retrieval-Augmented Question Answering (RAG)** using FAISS and an **open-source LLM (Llama 2, Falcon, Mistral, GPT-Neo, etc.)**. The system provides analytics, answers queries, and exposes a **FastAPI-based REST API** for easy interaction.  

---

## **Features**  
- **Processes hotel booking data from CSV**  
- **Performs analytics (revenue trends, cancellations, booking distribution, etc.)**  
- **Implements Retrieval-Augmented Q&A using FAISS & LLM**  
- **Exposes a FastAPI with endpoints for analytics & queries**  
- **Optimized for fast API responses using precomputed analytics & FAISS search**  

---

## **Project Structure**  
```
/hotel-booking-analysis/
│── app.py                  # FastAPI Implementation  
│── preprocess.py           # Data Preprocessing & Cleaning  
│── analytics.py            # Revenue Trends, Cancellations, Lead Time Analysis  
│── rag.py                  # FAISS + LLM for Query Answering  
│── requirements.txt        # Required Dependencies  
│── hotel_bookings.csv      # Sample Dataset  
│── README.md               # Project Documentation  
```

---

## **Installation & Setup**  

### **1. Clone the Repository**  
```bash
git clone https://github.com/[your-github-username]/hotel-booking-analysis.git
cd hotel-booking-analysis
```

### **2. Install Required Dependencies**  
```bash
pip install -r requirements.txt
```
Dependencies include:  
- `fastapi` (API framework)  
- `uvicorn` (ASGI server)  
- `pandas` (Data Processing)  
- `faiss-cpu` (Vector Search)  
- `sentence-transformers` (Embedding model for FAISS)  

### **3. Run the API Server**  
```bash
uvicorn app:app --reload
```
The server will start on **http://127.0.0.1:8000**  

---

## **API Endpoints**  

### **POST `/analytics`**  
Returns precomputed **revenue trends, cancellation rates, booking lead times, and geographical insights.**  

### **POST `/ask`**  
Retrieves answers from **precomputed analytics** or performs **retrieval-augmented Q&A using FAISS & LLM**.  

Example Request:  
```json
{
  "question": "What is the total revenue?"
}
```
Example Response:  
```json
{
  "answer": "The total revenue is $83,495,957.98."
}
```

Example Request:  
```json
{
  "question": "Which locations had the highest booking cancellations?"
}
```
Example Response:  
```json
{
  "answer": "The highest booking cancellations were from Portugal."
}
```

---

## **Analytics Implemented**  

- **Revenue trends over time** (Monthly revenue calculations)  
- **Cancellation rate as a percentage of total bookings**  
- **Geographical distribution of bookings (Top countries)**  
- **Booking Lead time distribution (Average days before arrival)**  
- **Additional analytics (e.g., seasonal trends, most popular booking months)**  

---

## **Running API Tests**  

### **Using Swagger UI (Browser)**  
1. Open **http://127.0.0.1:8000/docs**  
2. Click on the `/ask` endpoint  
3. Enter a **question** (e.g., `"What is the total revenue?"`)  
4. Click "Execute" and check the response  

### **Using Python Requests**  
Run the following script:  
```python
import requests

url = "http://127.0.0.1:8000/ask"
data = {"question": "Which country had the most bookings?"}

response = requests.post(url, json=data)
print(response.json())
```
Expected Output:  
```json
{
  "answer": "The country with the most bookings is Portugal."
}
```
