Honeypot Network Threat Clustering with K-Means
Architecture Overview
This project implements an unsupervised threat detection pipeline using synthetic honeypot-generated data and the K-Means clustering algorithm. The process is organized into distinct steps:

Data Simulation
Generates realistic sessions simulating both attack and normal network traffic.
Captures details: source IP/country, protocol (SSH/HTTP), session duration, login attempts, command activity, and time of access.

Feature Engineering & Preprocessing
Computes behavioral and contextual features for each session:
Attack intensity, error rate, suspicious command ratio, command rate
Temporal indicators (hour of day, is_night, is_weekend)
Geographic risk and protocol encoding

Feature Scaling
Standardizes features for clustering analysis using z-score normalization.

K-Means Clustering
Segments all sessions into natural clusters based on interaction pattern and engineered features.
Automatically reveals groups corresponding to dominant attack or normal behaviors—no need for label supervision.

Cluster Analysis
Evaluates clusters for attack rate, common countries and protocols, and cluster size.
Maps clusters to "Attack" or "Normal" classifications.

Performance Evaluation
Displays accuracy, precision, recall and F1-score by matching clusters to true labels for validation.
Provides confusion matrices, per-cluster summaries, and visualization heatmaps.

Real-Time Threat Detection
Predicts the threat level of new incoming connections by assigning them to clusters and mapping cluster risk.

Engineered Features
attack_intensity = (connection_count × failed_login_attempts) / (session_duration + 1)
error_rate = failed_login_attempts / (connection_count + 1)
suspicious_ratio = suspicious_commands / (unique_commands + 1)
command_rate = unique_commands / (session_duration + 1)
Temporal: hour_of_day, day_of_week, is_night, is_weekend
Context: country_risk, protocol_ssh (binary indicators)

Results Highlights
K-Means clustering achieved clear separation of attack and normal sessions with a high accuracy (~99.9% in synthetic testing).
Cluster analysis revealed attack clusters (HTTP or SSH) with pure attack rate and normal clusters with near-zero false alarms.
Real-time detection mapped new connections successfully to appropriate risk levels.

Usage
Run the simulation to generate honeypot traffic data.
Apply feature engineering and scaling.

Train K-Means clustering and analyze clusters.

Use cluster assignment for real-time risk scoring.
