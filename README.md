# 🚀 IoT Information System for Autism Teacher Stress Assessment

A web-based information system using **Internet of Things (IoT)** and **DASS-21** methods to assess stress levels in autism support teachers.

## 📋 Key Features

### ✅ **1. DASS-21 Questionnaire**
- 7 standardized stress questions
- Likert Scale 0-3 (Never to Almost Always)
- Automatic score calculation per DASS-21 standards

### ✅ **2. IoT Sensor Integration**
- **Heart Rate** (Heart Rate Monitor) - 2x testing
- **Body Temperature** (Temperature Sensor) - 2x testing
- API endpoint for real-time sensor connection

### ✅ **3. Automatic Scoring**
DASS-21 score calculation with categories:
- **Category 0 - Normal**: Score 0-14 ✅
- **Category 1 - Mild**: Score 15-18 ⚠️
- **Category 2 - Moderate**: Score 19-25 🔶
- **Category 3 - Severe**: Score 26-33 🔴
- **Category 4 - Extremely Severe**: Score 34+ 🔴🔴

### ✅ **4. Analytics Dashboard**
- Stress distribution charts
- Real-time statistics
- Complete test results table
- Interactive visualization with Chart.js

## 🛠️ Technologies Used

### Backend
- **Python Flask** - Web framework
- **SQLite** - Database
- **RESTful API** - API architecture

### Frontend
- **Bootstrap 5** - UI framework
- **Chart.js** - Data visualization
- **Font Awesome** - Icons
- **Vanilla JavaScript** - Interactivity

## 📦 Installation

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run Server
```bash
python app.py
```

Server runs at: **http://localhost:5000**

## 🌐 Web Pages

### 1. **Home** (`/`)
- Landing page with system information
- Statistics overview
- Stress category explanation

### 2. **Start Test** (`/test`)
- Step 1: Respondent data input
- Step 2: IoT sensor data input
- Step 3: DASS-21 Questionnaire (7 questions)
- Step 4: Test results with recommendations

### 3. **Dashboard** (`/dashboard`)
- Complete statistics
- Bar, pie, and line charts
- All test results table
- Data filtering and sorting

## 🔌 API Endpoints

### Respondents
```
GET    /api/respondents          - Get all respondents
POST   /api/respondents          - Add new respondent
```

### Questions
```
GET    /api/questions            - Get DASS-21 questions
```

### Test
```
POST   /api/test                 - Submit test results
```

### Results
```
GET    /api/results              - Get all test results
GET    /api/results/<id>         - Get test result by respondent
```

### Statistics
```
GET    /api/statistics           - Get complete statistics
```

### IoT Sensor
```
POST   /api/iot/sensor           - Receive data from IoT sensors
```

## 📊 DASS-21 Calculation Method

### Step 1: Answer Questions
Each question has a scale:
- **0** = Never
- **1** = Sometimes
- **2** = Often
- **3** = Almost Always

### Step 2: Calculate Raw Score
```
Raw Score = Sum of all answers (0-21)
```

### Step 3: Convert to DASS-21 Score
```
Final Score = Raw Score × 2
```
*Multiplication by 2 for DASS-42 equivalence*

### Step 4: Determine Category
```
If Score <= 14  → Category 0 (Normal)
If Score 15-18  → Category 1 (Mild)
If Score 19-25  → Category 2 (Moderate)
If Score 26-33  → Category 3 (Severe)
If Score >= 34  → Category 4 (Extremely Severe)
```

### Calculation Example
```
Answers: [2, 1, 3, 2, 1, 2, 2]
Raw Score = 2+1+3+2+1+2+2 = 13
Final Score = 13 × 2 = 26
Category = 3 (Severe)
```

## 🔧 IoT Sensor Connection

To connect real IoT sensors:

### 1. Sensor Endpoint
Send sensor data to:
```
POST http://localhost:5000/api/iot/sensor
Content-Type: application/json

{
  "heart_rate": 118,
  "temperature": 31.5,
  "timestamp": "2026-04-14T10:30:00"
}
```

### 2. Arduino/ESP32 Code Example
```cpp
#include <WiFi.h>
#include <HTTPClient.h>

void sendSensorData() {
  WiFiClient client;
  HTTPClient http;
  
  http.begin(client, "http://YOUR_IP:5000/api/iot/sensor");
  http.addHeader("Content-Type", "application/json");
  
  String jsonData = "{\"heart_rate\":" + String(heartRate) + 
                    ",\"temperature\":" + String(temperature) + "}";
  
  int httpResponseCode = http.POST(jsonData);
  http.end();
}
```

## 📁 File Structure

```
final_project/
├── app.py                      # Flask backend application
├── requirements.txt            # Python dependencies
├── stress_test.db             # SQLite database (auto-created)
├── templates/
│   ├── index.html             # Landing page
│   ├── test.html              # Test page with questionnaire
│   ├── dashboard.html         # Analytics dashboard
│   └── demo.html              # System demo/documentation
├── README.md                  # This documentation
├── read_excel.py              # Excel reader script
├── analyze_dass21.py          # DASS-21 analysis script
└── test_app.py                # Test script
```

## 🎨 UI Design

The system uses modern design with:
- ✅ Attractive gradient backgrounds
- ✅ Card-based layout
- ✅ Smooth animations and transitions
- ✅ Responsive design (mobile-friendly)
- ✅ Interactive charts and graphs
- ✅ Color-coded stress categories
- ✅ Step-by-step wizard for testing

## 🔒 Security

- SQL Injection prevention with parameterized queries
- CORS enabled for API access
- Input validation on frontend and backend
- Protected SQLite database

## 📈 Development

For further development:

### Add DASS-21 Questions
Edit in `app.py`:
```python
DASS21_STRESS_QUESTIONS = [
    # Add new questions here
]
```

### Modify Category Thresholds
Edit `calculate_stress_category()` function in `app.py`

### Add Features
- Export data to Excel
- Email notification
- User authentication
- Real-time WebSocket for sensors
- Machine learning prediction

## 📞 Support

For questions or issues, please create an issue or contact the developer.

## 📄 License

MIT License - Free to use and modify

---

**Made with ❤️ for IoT and mental health research**

© 2026 IoT Stress Test System