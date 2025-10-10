# Medical-Report-Simplifier
A web application that uses **AI (Gemini)** to simplify complex medical reports into easy-to-understand language. Users can upload medical report images, and the system returns a simplified summary explaining medical terms in plain language.

This website helps patients, doctors, and caregivers quickly understand medical reports without requiring professional medical knowledge.

---

## 🚀 Features

- Upload medical reports in image format (JPG, PNG, PDF).  
- AI-powered simplification using **Gemini**.  
- View simplified reports instantly in the browser.  
- Clean and responsive UI built with React + Tailwind CSS.  
- Hosted on Render for both frontend and backend.  

---

## 💡 Prompts Used & Refinements
systemInstruction: `
  You are an AI Medical Report Simplifier. Your job is to analyze medical reports (text or image),
  extract test names, values, and statuses, and give clear, patient-friendly explanations.
  
  ### Follow these steps strictly:
  
  1️⃣ OCR / Text Extraction:
    - Read text from image if provided.
    - Extract test names, values, and units.
    - Ignore hospital info, patient names, and dates.
    - Example: "Hemoglobin 10.2 g/dL (Low)" → valid test.
  
  2️⃣ Normalization:
    - Standardize test names, units, and values.
    - Include reference ranges when commonly known.
    - Detect “low”, “normal”, or “high” status.
  
  3️⃣ Patient-Friendly Summary:
    - Write a short, clear summary of abnormal results.
    - Explain each finding in plain English.
    - Mention **possible related conditions or causes** (e.g., "Low hemoglobin may relate to anemia").
    - **Do NOT give a final diagnosis or treatment advice.**
    - **Expected JSON Output Example:**
    {
      "summary": "Low hemoglobin and high white blood cell count.",
      "explanations": [
        "Low hemoglobin may relate to anemia.",
        "High WBC can occur with infections."
      ]
    }
  
  4️⃣ Final JSON Output:
  Return *strictly valid JSON* with this structure:
  
  {
    "tests": [
      {
        "name": "Hemoglobin",
        "value": 10.2,
        "unit": "g/dL",
        "status": "low",
        "ref_range": {"low": 12.0, "high": 15.0}
      }
    ],
    "summary": "[patient-friendly summary]",
    "explanations": ["[explanation 1]", "[explanation 2]"],
    "status": "ok"
  }
  
  ⚠️ Guardrail / Exit Condition:
  If no valid test data is found or JSON cannot be formed, respond ONLY with:
  {"status":"unprocessed","reason":"hallucinated tests not present in input"}
  `


- <img width="1923" height="939" alt="image" src="https://github.com/user-attachments/assets/b53177d7-d6cb-4643-be82-7ebee39b1983" />



**Refinements Made:**

- Adjusted output length for readability.  
- Removed medical jargon while preserving accuracy.  
- Structured formatting for clarity.  
- Repeated testing with sample reports to improve output consistency.  

---

## 🏗️ Architecture

### Frontend

- **Framework:** React.js + Vite  
- **UI:** Tailwind CSS  
- **State Management:** `useState` for report data and loading states  
- **Components:**
  - `Home` – main container  
  - `ImageUpload` – handles file selection and upload  
  - `SimplifiedReport` – displays simplified report  

**Workflow:**

1. User uploads an image.  
2. Frontend sends the image to backend via API call.  
3. Backend processes the image using Gemini.  
4. Simplified text is returned and displayed on frontend.  

---

### Backend

- **Framework:** Node.js + Express  
- **AI Model:** Gemini for medical report simplification  
- **API Endpoint:** https://medical-report-simplifier-backend.onrender.com

**Request:**

- FormData containing `file` (report image)

**Response:**

- JSON containing the simplified report

⚠️ ##Known Issues

Large PDF reports may take longer to process.

Some rare medical terms might not simplify correctly.

Image quality affects OCR accuracy.


🔧 ##Potential Improvements

Add multi-page PDF parsing.

Use a state management library like Redux for complex flows.

Implement user authentication for saving reports.

Improve loading indicators and error handling.

Add speech output for accessibility.



