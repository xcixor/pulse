# Period Pulse

---

### **Project Requirements & Specifications Document** 

**Project Title:** "Period Pulse" \- An Open-Source Social Media Analytics Dashboard for Menstrual Health Initiatives in Kenya

**Project Goal:** To build a user-friendly, web-based dashboard that provides actionable, geographical insights from social media data to assist non-technical users in the non-profit sector. The tool will help them understand public sentiment, identify key topics of conversation, and receive timely alerts and summaries related to sanitary pads and menstruation.

**Target User:** Non-technical individuals, such as non-profit organizers, volunteers, and community leaders.

---

#### **1\. Core Objectives**

The primary objectives of this project are:

* **Data Collection:** To programmatically collect text data from Twitter and Facebook related to menstrual health in Kenya.  
* **Custom ML Model Development:** To build and train a custom sentiment analysis model that is specifically tailored to the nuances of local language, slang, and context in Kenya.  
* **Geospatial Analysis:** To link social media posts to specific geographical locations (e.g., counties or cities) within Kenya.  
* **Interactive Web Dashboard:** To create a modern, interactive web application that visualizes the analyzed data in an intuitive and easily understandable format.  
* **Actionable Alerts & Reporting (Nice-to-Haves):** To implement features that provide immediate notifications for critical events and generate periodic summary reports for strategic planning.

---

#### **2\. Technical Specifications**

This section outlines the specific components, tools, and technologies required to build the project.

**2.1. Data Collection & Processing Pipeline**

* **Data Sources:** Twitter and Facebook.  
* **Data Collection Tools:**  
  * **Twitter API:** To stream and collect tweets based on specific keywords.  
  * **Facebook API/Scraper:** To collect public posts and comments, with careful consideration of platform terms of service.  
* **Data Preprocessing:**  
  * **Text Cleaning:** Removal of URLs, mentions, emojis, and special characters.  
  * **Tokenization & Normalization:** Splitting text into words and converting to a standard format.  
  * **Language & Slang Handling:** Handling of code-switching between English, Swahili, and Sheng.

**2.2. Machine Learning Model**

* **Model Type:** A supervised text classification model.  
* **Task 1: Sentiment Analysis:**  
  * **Objective:** To classify posts into three categories: Positive, Negative, and Neutral.  
  * **Process:** Manually label a collected dataset and train a custom classifier using scikit-learn, Keras, or PyTorch.  
* **Task 2: Geographical Extraction:**  
  * **Objective:** To extract location information from the social media posts.  
  * **Process:** Analyze tweet metadata and use Named Entity Recognition (NER) to identify place names, mapping them to Kenyan counties.  
* **Task 3: Keyword/Topic Identification (Advanced ML):**  
  * **Objective:** To identify the core topic of a conversation (e.g., "stockout," "cost," "distribution drive").  
  * **Process:** Use a clustering or topic modeling algorithm (like LDA) on the post text to automatically group similar conversations. This is a crucial component for the "real-time alarm" feature.

**2.3. Backend & API**

* **Backend Framework:** Python-based, using Flask or FastAPI.  
* **Database:** PostgreSQL or SQLite to store the analyzed data (post text, sentiment, topic, location, timestamp).  
* **API Endpoints:**  
  * /api/sentiment\_data: Returns all analyzed data.  
  * /api/sentiment\_by\_location: Returns sentiment breakdown for a specific county.  
  * /api/trends: Returns a list of trending topics.  
  * /api/alarms: (New) An endpoint for the real-time alarm feature.  
  * /api/reports: (New) An endpoint for the weekly summary reports.

**2.4. Frontend (Dashboard)**

* **Framework:** Next.js and React.  
* **Key Dashboard Features:**  
  1. **Geographical Map:** A map of Kenya (e.g., using Leaflet or Mapbox) color-coded by sentiment and zoomable to show individual posts.  
  2. **Sentiment Breakdown:** A component showing the overall percentage of positive, negative, and neutral posts.  
  3. **Trending Topics:** A word cloud or a list of the most frequent keywords.  
  4. **Raw Data View:** A table showing the actual posts, their sentiment, and location.

**2.5. Additional Features (Nice-to-Haves)**

* **Real-time Alarms (Option A):**  
  * **Description:** A system that sends immediate notifications when a post with a negative sentiment and a specific critical keyword (e.g., "stockout," "no pads," "expensive") is detected.  
  * **Implementation:** The backend will need to run a continuous job that listens for new social media posts. When a post matches the criteria, it will trigger a notification.  
  * **Interface:** The dashboard could have a dedicated "Alerts" section, and a simple push notification could be implemented using web sockets or a tool like Socket.IO. The alert would link directly to the post on the map.  
* **Weekly Summary Reports (Option B):**  
  * **Description:** An automated weekly email or PDF report summarizing the data from the past seven days.  
  * **Implementation:**  
    1. **Reporting Script:** A backend script would run once a week (e.g., every Sunday night).  
    2. **Data Aggregation:** The script would query the database to aggregate data for the week: overall sentiment trend, top 5 negative keywords, top 5 positive keywords, and a summary of sentiment by location.  
    3. **Report Generation:** The script would use a library (e.g., ReportLab for Python) to generate a PDF report with text and visualizations.  
  * **Interface:** A simple "Reports" section on the dashboard could store a history of these generated reports.

#### **3\. High-Level Project Plan & Milestones**

1. **Phase 1: Foundation (Weeks 1-3):**  
   * Set up the development environment, APIs, and database.  
   * Build a basic data collection script.  
2. **Phase 2: Machine Learning Core (Weeks 4-8):**  
   * Begin data labeling and develop the custom sentiment analysis model.  
   * Implement location extraction logic.  
   * Integrate the ML models into a backend API.  
3. **Phase 3: Frontend Development (Weeks 9-12):**  
   * Build the core Next.js/React dashboard with the map, charts, and data view.  
4. **Phase 4: "Nice-to-Have" Features (Weeks 13-16):**  
   * Develop the real-time alarm system (backend script and frontend alerts).  
   * Build the weekly summary report generation script and integrate it into the dashboard.  
5. **Phase 5: Testing & Deployment (Weeks 17-20):**  
   * Thoroughly test all components, from data collection to reporting.  
   * Deploy the application and gather feedback from the target user.

