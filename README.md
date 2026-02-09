

# 🚀 Autonomous Insurance Claims Processing Agent

Rule-based autonomous insurance claims processing agent that extracts FNOL data, validates fields, and routes claims intelligently.

---

## 📌 Problem Statement

Build a lightweight agent that:

- Extracts key fields from FNOL (First Notice of Loss) documents  
- Identifies missing or inconsistent fields  
- Classifies and routes claims to the correct workflow  
- Provides a short explanation for the routing decision  

---

## 🧠 Solution Overview

This project implements a rule-based Autonomous Insurance Claims Processing Agent using Python.

The system processes structured ACORD FNOL PDF forms and generates structured JSON output:

{
  "extractedFields": {},
  "missingFields": [],
  "recommendedRoute": "",
  "reasoning": ""
}

---

## 🔎 Key Features

### 1️⃣ Field Extraction

- Extracts structured form field data using pypdf
- Dynamically detects accident description
- Handles editable ACORD PDF forms

### Extracted Categories

Policy Information:
- Policy Number  
- Policyholder Name  
- Effective Dates  

Incident Information:
- Date  
- Time  
- Location  
- Description  

Involved Parties:
- Claimant  
- Third Parties  
- Contact Details  

Asset Details:
- Asset Type  
- Asset ID  
- Estimated Damage  

Other Mandatory Fields:
- Claim Type  
- Attachments  
- Initial Estimate  

---

## ✅ Missing Field Validation

Mandatory fields checked:

- Policy Number  
- Policyholder Name  
- Date  
- Location  
- Description  
- Estimated Damage  
- Claim Type  

Invalid values such as:
- None  
- ""  
- "N/A"  
- "NA"  

are treated as missing.

---

## 🚦 Routing Logic (Priority Order)

1. If mandatory fields are missing → Manual Review  
2. If description contains "fraud", "staged", "inconsistent" → Investigation Flag  
3. If description contains "injury" or "injured" → Specialist Queue  
4. If estimated damage < 25,000 → Fast-track  
5. Otherwise → Manual Review (High Damage Value)

---

## 📂 Test Cases

| File | Scenario | Expected Route |
|------|----------|---------------|
| File 1 | Clean claim (<25k) | Fast-track |
| File 2 | Missing fields | Manual Review |
| File 3 | Fraud keywords | Investigation Flag |
| File 4 | Injury case | Specialist Queue |

All four scenarios validated successfully.

---

## 🛠 Technologies Used

- Python  
- pypdf  
- Rule-based workflow engine  
- JSON structured output  

---

## ▶ How to Run

1. Install dependency:

pip install pypdf

2. Open claims_agent.ipynb  
3. Run all cells  

---

## 📌 Example Output

{
  "extractedFields": {...},
  "missingFields": [],
  "recommendedRoute": "Fast-track",
  "reasoning": "Estimated damage below 25,000."
}

---

## 💡 Future Enhancements

- NLP-based classification instead of keyword rules  
- OCR support for scanned PDFs  
- ML-based fraud detection  
- REST API deployment using FastAPI  
- Cloud deployment  

---

## 🎯 Conclusion

This solution demonstrates:

- Structured PDF form processing  
- Field validation  
- Intelligent workflow routing  
- Clean JSON output design  
- Extensible architecture  

The system simulates a real-world autonomous insurance claims workflow engine.

