# Requirements - ReportGuru: Radiology Report Intelligence

## Introduction

ReportGuru is a patient-facing AI platform that makes radiology reports understandable for every Indian citizen. India conducts over 30 crore radiology tests annually, yet most patients cannot comprehend the medical jargon in their reports. Patients panic, misinterpret findings, delay treatment, or make uninformed decisions.

Unlike existing solutions (ChatGPT, 1mg, Practo) that can only explain report *text*, ReportGuru performs **multi-modal analysis** — correlating actual medical images (X-ray, MRI, CT scans in DICOM format) with radiologist report text. It highlights abnormal areas directly on the scan, validates the radiologist's findings against the image, explains everything in simple Hindi/English, and tracks health progression over time.

**Track:** Healthcare & Life Sciences (Professional/Startup Track)

**Target Users:** Indian patients and their families, diagnostic labs, hospitals, telemedicine platforms.

**Key Differentiator:** Specialized computer vision on medical images + LLM-powered text interpretation + cross-validation correlation engine. This cannot be replicated by generic AI chatbots.

---

## Requirements

### 1. Medical Image Upload & Processing

**User Story:** As a patient, I want to upload my radiology scan images (X-ray, MRI, CT) so that the system can analyze them visually alongside my report.

#### Acceptance Criteria (EARS Format)

1. WHEN a user uploads a medical image in DICOM format THE SYSTEM SHALL parse and extract the image data using a DICOM parser and display a preview within 5 seconds.
2. WHEN a user uploads a medical image in common formats (JPEG, PNG, PDF) THE SYSTEM SHALL accept and process the image for visual analysis.
3. WHEN an uploaded image is corrupted or in an unsupported format THE SYSTEM SHALL display a clear error message in the user's selected language and suggest supported formats.
4. WHEN a user uploads multiple images (e.g., multiple MRI slices) THE SYSTEM SHALL process all images and present them in a navigable gallery view.
5. WHEN image upload is complete THE SYSTEM SHALL store the image securely with encryption at rest, compliant with ABDM (Ayushman Bharat Digital Mission) data standards.

---

### 2. Radiology Report Text Ingestion

**User Story:** As a patient, I want to upload my radiology report (PDF, image, or typed text) so that the system can extract and interpret the medical findings.

#### Acceptance Criteria (EARS Format)

1. WHEN a user uploads a radiology report as a scanned PDF or image THE SYSTEM SHALL perform OCR to extract the text content with at least 95% accuracy.
2. WHEN a user uploads a digitally generated PDF report THE SYSTEM SHALL extract text directly without OCR.
3. WHEN a user types or pastes report text manually THE SYSTEM SHALL accept free-text input for analysis.
4. WHEN the report text is extracted THE SYSTEM SHALL perform Medical Named Entity Recognition (NER) to identify findings, diagnoses, measurements, and anatomical references.
5. WHEN OCR extraction confidence is below 90% THE SYSTEM SHALL flag low-confidence sections and prompt the user to verify or re-upload.

---

### 3. AI-Powered Medical Image Analysis (Vision Engine)

**User Story:** As a patient, I want the AI to analyze my actual scan image and identify abnormal areas so that I can visually see what the radiologist is referring to.

#### Acceptance Criteria (EARS Format)

1. WHEN a medical image is processed THE SYSTEM SHALL use computer vision models (U-Net segmentation, ResNet classification) to detect and segment organs, lesions, and abnormal regions.
2. WHEN abnormalities are detected in the image THE SYSTEM SHALL generate color-coded overlays: red for abnormal/concerning areas, yellow for areas requiring monitoring, and green for healthy regions.
3. WHEN the image analysis is complete THE SYSTEM SHALL provide quantitative measurements (e.g., lesion size in mm, heart diameter, lung field area) and compare them against normal reference ranges.
4. WHEN a user views the analyzed image THE SYSTEM SHALL display interactive overlays that can be toggled on/off for each finding category.
5. WHEN the vision engine encounters an image modality it cannot analyze with confidence THE SYSTEM SHALL inform the user of limitations and recommend consulting a specialist.

---

### 4. Report-Image Cross-Validation (Correlation Engine)

**User Story:** As a patient, I want the system to verify that what the radiologist wrote in the report matches what is visible in the actual scan so that I have greater confidence in my diagnosis.

#### Acceptance Criteria (EARS Format)

1. WHEN both the medical image and report text are analyzed THE SYSTEM SHALL correlate text findings with detected image regions (e.g., "bilateral opacities" in report → confirmed in both lung fields of the image).
2. WHEN the image analysis confirms a report finding THE SYSTEM SHALL display a green checkmark (✅) with confidence score next to the validated finding.
3. WHEN the image analysis contradicts or cannot confirm a report finding THE SYSTEM SHALL display a warning flag (⚠️) and suggest the patient seek a second opinion or re-review.
4. WHEN cross-validation is complete THE SYSTEM SHALL generate an overall correlation confidence score (0-100%) for the entire report.
5. WHEN a mismatch is detected between report findings and image analysis THE SYSTEM SHALL clearly explain the discrepancy in simple language without causing panic.

---

### 5. Patient-Friendly Explanation Generation

**User Story:** As a patient with limited medical knowledge, I want to receive a simple, jargon-free explanation of my report and scan findings in my preferred language so that I understand my health condition clearly.

#### Acceptance Criteria (EARS Format)

1. WHEN analysis is complete THE SYSTEM SHALL generate a patient-friendly explanation in simple language (default: Hindi and English) at an 8th-grade reading level.
2. WHEN medical terms are used in the explanation THE SYSTEM SHALL provide inline definitions and real-world size/severity comparisons (e.g., "5mm = smaller than a pencil eraser").
3. WHEN the explanation is generated THE SYSTEM SHALL include a clear severity indicator (Normal / Mild / Moderate / Severe / Critical) with appropriate color coding.
4. WHEN findings require follow-up THE SYSTEM SHALL generate a prioritized, actionable step list (e.g., "Consult cardiologist this week", "Follow-up X-ray in 2 weeks").
5. WHEN a user selects a regional language preference THE SYSTEM SHALL provide the explanation in the selected Indic language (Hindi, Tamil, Telugu, Kannada, Bengali, Marathi — Phase 1).
6. WHEN the user is elderly or has accessibility needs THE SYSTEM SHALL offer a voice-narrated explanation using text-to-speech in the selected language.

---

### 6. Scan Progression Tracking & Health Timeline

**User Story:** As a patient with a chronic condition, I want to compare my current scan with previous scans so that I can track whether my condition is improving, stable, or worsening.

#### Acceptance Criteria (EARS Format)

1. WHEN a user uploads a new scan and has previous scans stored THE SYSTEM SHALL automatically identify the same scan type and body region for comparison.
2. WHEN comparison scans are available THE SYSTEM SHALL display a side-by-side view with aligned orientations and highlighted differences.
3. WHEN quantitative measurements exist across multiple scans THE SYSTEM SHALL generate a timeline chart showing progression (e.g., tumor size over months, creatinine levels trend).
4. WHEN progression shows worsening trends THE SYSTEM SHALL generate an alert with urgency-appropriate language and recommended actions.
5. WHEN a user accesses the health timeline THE SYSTEM SHALL display a chronological view of all uploaded scans, reports, and key findings per family member.

---

### 7. Second Opinion & Doctor Sharing Package

**User Story:** As a patient seeking a second opinion, I want to generate a structured summary of my AI-analyzed report and scan that I can share with another doctor so that they can quickly understand my case.

#### Acceptance Criteria (EARS Format)

1. WHEN a user requests a second-opinion package THE SYSTEM SHALL generate a structured clinical summary including: original report, AI image analysis with annotated overlays, quantitative measurements, and progression data.
2. WHEN the package is generated THE SYSTEM SHALL format it in a doctor-friendly layout with medical terminology preserved alongside patient-friendly explanations.
3. WHEN a user chooses to share the package THE SYSTEM SHALL provide sharing options: secure link, PDF download, or direct integration with telemedicine platforms (Practo, Apollo 24/7).
4. WHEN a shared link is accessed by a doctor THE SYSTEM SHALL require authentication and log access for audit purposes.

---

### 8. Secure Data Storage & ABDM Compliance

**User Story:** As a patient, I want my medical images and reports stored securely with proper privacy protections so that my health data is safe and compliant with Indian health data regulations.

#### Acceptance Criteria (EARS Format)

1. WHEN medical data is stored THE SYSTEM SHALL encrypt all data at rest (AES-256) and in transit (TLS 1.3).
2. WHEN the user links their ABHA (Ayushman Bharat Health Account) ID THE SYSTEM SHALL sync data with the ABDM Health Locker ecosystem.
3. WHEN a user requests data deletion THE SYSTEM SHALL permanently delete all associated images, reports, and analysis results within 48 hours and provide confirmation.
4. WHEN the system stores or processes medical images THE SYSTEM SHALL maintain HIPAA-grade security practices and comply with India's Digital Personal Data Protection Act (DPDPA) 2023.
5. WHEN any data access or modification occurs THE SYSTEM SHALL log the event in an immutable audit trail.

---

### 9. User Authentication & Onboarding

**User Story:** As a new user, I want to sign up quickly and start analyzing my first report within minutes so that I don't face barriers to accessing the service.

#### Acceptance Criteria (EARS Format)

1. WHEN a new user opens the app THE SYSTEM SHALL offer sign-up via mobile OTP (primary), Google, or ABHA ID.
2. WHEN a user signs up for the first time THE SYSTEM SHALL present a guided onboarding flow (3 steps max) showing how to upload a scan and report.
3. WHEN a user completes authentication THE SYSTEM SHALL create a secure session with JWT tokens and support session persistence across devices.
4. WHEN a user selects their preferred language during onboarding THE SYSTEM SHALL persist the preference and apply it across all explanations and UI elements.

---

## Success Metrics

- **Report comprehension:** 90%+ of users report understanding their radiology findings after using ReportGuru (measured via in-app survey).
- **Cross-validation accuracy:** 85%+ correlation accuracy between AI image analysis and radiologist report findings.
- **Time to explanation:** < 30 seconds from upload to patient-friendly explanation for standard X-rays.
- **User retention:** 60%+ users return for subsequent scan analysis within 6 months.
- **Language coverage:** Support for 6+ Indic languages within Phase 1.

## Constraints

- Medical image AI models require GPU infrastructure for inference (target: AWS EC2 P-series or SageMaker endpoints via Amazon Bedrock).
- DICOM processing libraries and medical CV models (U-Net, ResNet) require specialized training on Indian radiology datasets.
- The system provides educational explanations only — it must **not** position itself as a diagnostic replacement for qualified radiologists. All outputs must include a medical disclaimer.
- Initial launch targets chest X-rays and brain MRI as primary modalities; other modalities will be added incrementally.
- Must comply with DPDPA 2023, ABDM guidelines, and medical device regulations (CDSCO) as applicable.

## Out of Scope

- Real-time diagnosis or treatment prescription (the system is an educational/explanatory tool, not a diagnostic device).
- Integration with hospital EMR/HIS systems (Phase 2+).
- Pathology, blood test, or non-radiology report analysis (future scope).
- Offline-first mode (requires internet for AI inference).
- Direct appointment booking with doctors (will integrate with existing platforms instead).
