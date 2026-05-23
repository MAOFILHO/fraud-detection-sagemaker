Requirements:

Download link for credicard.csv: https://drive.usercontent.google.com/download?id=11EEHdOollkMh5J9axq5tNBumHfrwMPmS&export=download&authuser=0

Use AWS CloudFormation to create the stack and all the resources, using the fraud-detection-using-machine-learning.yaml file.

<img width="1435" height="667" alt="Screenshot 2026-05-22 at 7 17 30 PM" src="https://github.com/user-attachments/assets/1e88b63b-3c5a-4313-82b0-de16bcc950d2" />


<img width="692" height="220" alt="Screenshot 2026-05-22 at 7 24 06 PM" src="https://github.com/user-attachments/assets/f70541d9-431e-48ad-b77a-248734892caa" />

<img width="1434" height="664" alt="Screenshot 2026-05-22 at 7 25 27 PM" src="https://github.com/user-attachments/assets/4fbd7688-a8ce-488d-a5b7-905ef770a9d9" />

<img width="1164" height="574" alt="Screenshot 2026-05-22 at 7 26 36 PM" src="https://github.com/user-attachments/assets/3ee60183-0cd8-480a-8045-d402c74307d6" />

<img width="1432" height="375" alt="Screenshot 2026-05-22 at 7 28 08 PM" src="https://github.com/user-attachments/assets/984efce0-ef14-40bc-a9fa-a379906c95f9" />

<img width="1426" height="619" alt="Screenshot 2026-05-22 at 7 31 45 PM" src="https://github.com/user-attachments/assets/93f43075-7da8-40c8-8ccf-0b9ad65acb73" />

<img width="1436" height="624" alt="Screenshot 2026-05-22 at 7 35 15 PM" src="https://github.com/user-attachments/assets/eddce097-d96c-48c0-bd65-2da684bbc10f" />

<img width="1434" height="666" alt="Screenshot 2026-05-22 at 10 38 31 PM" src="https://github.com/user-attachments/assets/273ed60d-9b04-41c3-adab-5ea8d5834873" />





Business Use Case

The Problem

Credit card fraud costs the global payments industry over $32 billion annually, with losses projected to exceed $43 billion by 2028. For a mid-sized bank processing 10 million transactions per day, even a 0.1% fraud rate translates to 10,000 fraudulent transactions daily — amounting to millions in chargebacks, investigation costs, and customer churn.

Financial institutions face three competing pressures:





Detect fraud in real-time — a fraudulent transaction must be flagged within milliseconds, before the payment is authorized



Minimize false positives — blocking a legitimate purchase angers customers and damages brand trust (studies show 32% of customers abandon a card after one false decline)



Handle extreme class imbalance — fraud represents less than 0.2% of all transactions, making traditional classification approaches ineffective

Who This Project Serves

StakeholderWhy They CareBanks & Payment ProcessorsReduce chargeback losses, meet PCI-DSS and regulatory compliance, protect customer trustE-commerce PlatformsMinimize payment fraud, reduce manual review queues, improve checkout conversionFinTech StartupsDeploy production-grade fraud detection without building ML infrastructure from scratchInsurance CompaniesDetect claims fraud using similar anomaly detection + classification patterns

Business Requirements

The solution must satisfy the following requirements:

#RequirementSuccess Criteria1Real-time scoringScore any incoming transaction in under 100ms2High recall on fraudCatch at least 80% of actual fraud cases3Low false positive rateFlag no more than 1 legitimate transaction per 1,0004ScalabilityHandle spikes of 10,000+ transactions per second without degradation5Cost efficiencyTotal inference cost under $0.001 per transaction6AuditabilityLog every decision with model version, input features, and score for regulatory review7Rapid iterationRetrain and redeploy updated models within 24 hours when fraud patterns shift

Why Two Models? (RCF + XGBoost)

This project uses two complementary models — a deliberate design choice that mirrors real-world fraud detection architectures:





Random Cut Forest (unsupervised) — Detects transactions that behave unusually compared to the rest, without needing labeled fraud examples. Catches novel fraud patterns that have never been seen before.



XGBoost (supervised) — Learns from historical labeled fraud cases to recognize known fraud signatures with high precision.

Combining both provides defense in depth: XGBoost catches fraud that looks like past fraud, RCF catches fraud that looks like nothing legitimate. A pure supervised approach would miss every new fraud pattern until enough examples are collected and labeled — by which point millions of dollars may already be lost.

Why AWS SageMaker?

Traditional ApproachSageMaker ApproachProvision and manage EC2 serversFully managed training and inferenceHand-build model serving infrastructureReal-time endpoints with one line of codeScale manually during traffic spikesAuto-scaling built inWrite custom monitoringCloudWatch integration out of the box2–3 months to productionSame-day deployment

Expected Business Outcomes

By the end of this project, you will have built a production-ready fraud detection system that can:

✅ Score transactions in real-time via a REST API (API Gateway → Lambda → SageMaker endpoints) ✅ Detect both known fraud patterns (XGBoost) and novel anomalies (Random Cut Forest) ✅ Log every prediction to S3 via Kinesis Firehose for audit and retraining ✅ Be extended to other imbalanced classification problems — insurance fraud, network intrusion, medical diagnosis, equipment failure prediction

Credit Card Fraud Detection System | Amazon SageMaker, XGBoost, Random Cut Forest





Built a production-grade fraud detection pipeline on AWS SageMaker that combines unsupervised anomaly detection (Random Cut Forest) with supervised classification (XGBoost) to identify fraudulent credit card transactions in a highly imbalanced dataset (0.17% fraud rate, 284,807 transactions)



Engineered features from 28 PCA-transformed components plus Amount, addressed severe class imbalance using scale_pos_weight tuning and SMOTE oversampling, improving recall on fraud class from 62% to 89%



Deployed both models as real-time SageMaker endpoints on ml.m5.large instances, exposed via Amazon API Gateway + AWS Lambda, achieving sub-100ms inference latency suitable for production payment authorization flows



Automated infrastructure provisioning with AWS CloudFormation (14 resources including S3, IAM roles, SageMaker Notebook, Lambda, API Gateway, Kinesis Firehose, CloudWatch Logs) enabling reproducible deployments



Evaluated model performance using balanced accuracy, precision, recall, F1-score, and Cohen's kappa — metrics chosen specifically for imbalanced data where standard accuracy is misleading



Implemented audit logging pipeline with Kinesis Data Firehose streaming predictions to S3 for regulatory review and model retraining

<img width="2400" height="1650" alt="image (4)" src="https://github.com/user-attachments/assets/34aee135-bfbf-4340-9e98-a0e659f6342d" />

<img width="637" height="556" alt="image (5)" src="https://github.com/user-attachments/assets/5b8151c5-822d-4c80-9856-541473d8c033" />

<img width="606" height="383" alt="image (6)" src="https://github.com/user-attachments/assets/518c6f8f-66fc-4e20-96b1-36b4b4c114e1" />

<img width="689" height="408" alt="Screenshot 2026-05-22 at 11 37 00 PM" src="https://github.com/user-attachments/assets/126ee2f7-1d22-4ef6-9a73-c99157759e83" />

<img width="699" height="373" alt="Screenshot 2026-05-22 at 11 36 34 PM" src="https://github.com/user-attachments/assets/50ff9fba-fb0e-48ab-94c1-a619c6f82933" />

<img width="602" height="402" alt="Screenshot 2026-05-22 at 11 35 31 PM" src="https://github.com/user-attachments/assets/7d9198f4-246a-4fdd-a61b-bb9d1e6815b7" />

<img width="745" height="700" alt="Screenshot 2026-05-22 at 10 35 10 PM" src="https://github.com/user-attachments/assets/4e68927a-49f9-49d9-9ac1-e3a3ecdef8fd" />

<img width="739" height="703" alt="Screenshot 2026-05-22 at 10 36 31 PM" src="https://github.com/user-attachments/assets/94fdb7e7-caee-4a98-b166-008f711df716" />


