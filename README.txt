Job Application Chatbot
Overview
The Job Application Chatbot is a Python-based application designed to streamline job applications by allowing users to explore job roles, upload resumes (PDF or text), and receive qualification feedback. It features multilingual resume parsing (English and Hindi), confidence-based job matching, and a conversational interface. Built with modularity and extensibility in mind, it leverages NLP techniques via OpenAI’s gpt-4o-mini for resume parsing and supports transliteration for Hindi resumes.
This project fulfills the following objectives:

Conversational chatbot for job applications.
Resume parsing for key details (name, email, phone, skills, education, experience).
Qualification matching with confidence scoring.
Multilingual support (English + Hindi).
Modular code structure with clear separation of concerns.

Features
1. Chatbot Interaction Flow

Greeting and Confirmation: Initiates with a greeting ("Hi! I want to apply for a job.") and prompts the user to confirm interest in job roles ("Would you like to see available job roles?").
Job Role Listing: Displays three job roles with attributes:
Data Analyst: Requires Python, SQL, Data Visualization, Statistical Analysis; Bachelor’s in Statistics, Mathematics, or Computer Science; 2–4 years experience.
Developer: Requires Python, Java, JavaScript, Git, Agile; Bachelor’s in Computer Science or related; 3–5 years experience.
Tester: Requires Selenium, JUnit, Test Automation, Bug Tracking; Bachelor’s in Computer Science or equivalent; 1–3 years experience.


User Interaction: Guides users to select a role and confirm application intent.
Limitation: Uses simple string matching (yes/no, 1/2/3) instead of advanced NLP frameworks like Rasa or Dialogflow, limiting input flexibility.

2. Resume Upload & Parsing

Supported Formats: Accepts resumes in PDF (via PyPDF2) and text (UTF-8 encoded) formats using Colab’s file upload.
Data Extraction:
Name, Email, Phone: Extracts using regex and OpenAI’s gpt-4o-mini for robust parsing. Falls back to regex for name (English or transliterated Hindi) and contact details.
Skills: Identifies all skills and matches against job requirements using fuzzy matching (fuzzywuzzy, >80% similarity).
Education: Extracts degrees, institutions, and years, supporting transliterated Hindi terms (e.g., "bI.es.", "baichelor").
Experience: Extracts in "YYYY-YYYY: Job Title, Company" format, handling "Present" for ongoing roles.


Multilingual Support: Detects language (langdetect) and transliterates Hindi resumes to Latin script (indic_transliteration) for processing.
NLP Integration: Uses gpt-4o-mini for structured extraction, with regex as a fallback for robustness.

3. Information Confirmation & Finalization

Qualification Feedback: Computes a confidence score (40% skills, 30% education, 30% experience) to determine if the candidate qualifies (>50% threshold). Provides detailed feedback on skills, education, and experience matches.
Confirmation: Displays extracted details (name, email, phone, skills, education, experience) and asks for contact preference ("email/phone"). Handles missing contact info by prompting for alternatives.
Final Message: Concludes with a friendly message: "Thank you for applying! We'll review your application and get back to you."
Limitation: Confirmation focuses on contact method rather than verifying all extracted details. Negative response handling is minimal.

4. System Architecture & Code

Modularity: Organized into functions:
read_pdf/read_txt: File reading.
detect_and_transliterate: Language detection and Hindi transliteration.
extract_resume_details: Resume parsing with LLM and regex.
calculate_experience_years: Experience calculation.
check_qualification: Job matching with confidence scoring.
job_chatbot: Main interaction flow.


Separation of Concerns: Parsing, matching, and file handling are modular, but chatbot logic is in a single function, slightly reducing modularity.
Libraries:
PyPDF2: PDF parsing.
langdetect: Language detection.
indic_transliteration: Hindi transliteration.
fuzzywuzzy: Skill matching.
openai: Resume parsing via gpt-4o-mini.


Limitation: No API endpoints (e.g., for resume upload). Runs in Colab, not as a standalone service.

5. Bonus Features

Confidence Scoring: Implements a weighted score (skills: 40%, education: 30%, experience: 30%) with detailed feedback on mismatches.
LLM Parsing: Uses gpt-4o-mini for unstructured resume text, with regex fallback for robustness.
Multilingual Support: Fully supports English and Hindi resumes via transliteration and language-aware parsing.

Setup Instructions

Prerequisites:

Python 3.8+
Google Colab environment (or adapt for local use)
OpenAI API key (store as OpenAi in Colab Secrets)
Install dependencies:pip install PyPDF2 langdetect indic_transliteration fuzzywuzzy openai google-colab python-Levenshtein




Running the Application:

Clone the repository:git clone <repository-url>
cd <repository-name>


Open job_chatbot.py in Colab or a Python environment.
Set the OpenAI API key in Colab Secrets or as an environment variable:export OPENAI_API_KEY='your-api-key'


Run the script:python job_chatbot.py


Follow prompts to select a job role, upload a resume, and confirm details.


Usage:

Respond to the initial prompt ("Would you like to see available job roles?").
Select a job role (1–3).
Upload a PDF or text resume.
Review extracted details and choose a contact method.
Receive qualification feedback and a confirmation message.



Limitations

Chatbot: Limited to exact inputs (yes/no, 1/2/3). Lacks advanced NLP (e.g., Rasa, transformers) for flexible input handling.
APIs: No RESTful endpoints for resume upload or processing.
Documentation: No system design diagrams or video demo (planned for future updates).
Error Handling: Basic; relies on print statements rather than structured logging.

Future Improvements

Integrate Rasa for NLP-based input handling.
Add API endpoints using FastAPI for resume uploads.
Support additional languages (e.g., Spanish).
Create system design diagrams and a demo video.
Enhance error handling with logging and unit tests.

Challenges Faced

Multilingual Parsing: Handling Hindi resumes required robust transliteration and regex adjustments for terms like "kaushal" (skills).
LLM Dependency: Reliance on gpt-4o-mini increases costs; regex fallback mitigates but isn’t as flexible.
Resume Variability: Non-standard resume formats (e.g., missing sections, varied date formats) required careful regex and LLM prompt design.

License
MIT License. See LICENSE for details.
