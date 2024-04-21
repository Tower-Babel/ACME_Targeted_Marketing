# Transforming Data into Targeted Marketing: A Cloud solution

## Abstract
ACME Inc., as a company, relies on mass-marketing strategies by leveraging its customer database for targeted campaigns. We present a Cloud-based Machine-Learning solution given an existing customer dataset that clusters and identifies exiting customers to cross-sell to. The infrastructure allows for remote analysis, scalability, and customizable trained models that can be used in a production setting.

## Introduction
Over time, ACME has become limited with its manual process and basic statistical techniques to analyze customer datasets. In-house segmentation based on demographics and historical data lacks effectiveness. ACME cannot access big data generated from social media, website interactions, and large volumes of transaction history, leading to incomplete insights. With a vision to transform big data into targeted marketing, an effective schema emerged in five parts: 
- Ingest
- Store
- Process & Analyze
- Build and Deploy ML*
- Monitor and Improve

## Our Approach
The ideology behind our approach focuses on designing data processing systems, building, and operationalizing data processing systems, operationalizing machine learning models, and ensuring solution quality. Designing data processing systems involved selecting storage technologies, including rational and analytical databases such as S3 simple storage service, elastic block store, and Elastic file system. Keeping in mind the business requirements, S3 buckets allowed us to map semi-structured data and schemas for relational databases. To build and operationalize data processing, we needed to support storage systems, pipelines, and infrastructure in a production environment. This will include migrating the data in a batch process. We used Amazon Glue to achieve this and to cover other common operations such as data ingestion, data cleaning, transformation, and integrating data with other sources. Machine Learning capabilities were an important element of our migration to the cloud. Prebuilt machine learning models available on Amazon and Hugging-face allowed us to deploy models efficiently, as well as training and evaluating models. The last element achieved in this approach included ensuring solution quality, which includes security, scalability, efficiency, and reliability. ACME now can go beyond simple segmentation, using in-house analysis methods based on demographic or just historical data. The portable solutions allow for resources to scale as needed.

## Core Functionality
Looking at the business requirements, ACME data gets migrated from on-premises file storage location to S3 bucket using batch ingestion mode and pushed in bulk using web-based API call. The following describes ACME current data fields:
- fullVisitorId: A unique identifier for each user of the Merchandise Store.
- channelGrouping: The channel via which the user came to the Store.
- date: The date on which the user visited the Store.
- device: The specifications for the device used to access the Store.
- geoNetwork: This section contains information about the geography of the user.
- socialEngagementType: Engagement type, either "Socially Engaged" or "Not Socially Engaged".
- totals: This section contains aggregate values across the session.
- trafficSource: This section contains information about the Traffic Source from which the session originated.
- visitId: An identifier for this session. This is part of the value usually stored as the _utmb cookie. This is only unique to the user. For a completely unique ID, you should use a combination of fullVisitorId and visitId.
- visitNumber: The session number for this user. If this is the first session, then this is set to 1.
- visitStartTime: The timestamp (expressed as POSIX time).
- hits: This row and nested fields are populated for any and all types of hits. Provides a record of all page visits.
- customDimensions: This section contains any user-level or session-level custom dimensions that are set for a session. This is a repeated field and has an entry for each dimension that is set.
- totals: This set of columns mostly includes high-level aggregate data.
#
(Real data taken from: [Google Analytics Customer Revenue Prediction](https://www.kaggle.com/competitions/ga-customer-revenue-prediction/data)) 
#
The transaction data was collected from applications and stored in a file system. By modern standards, the 35.9 GB dataset is relatively small. This data will be exported for use by the machine learning pipeline. The last field “totals” is the target attribute that ACME uses in the ML model to predict. The S3 bucket allows the data to be available for transformation and analysis. This storage allows for concurrency, collaboration, and version control. Amazon Lambda function triggers AWS Glue job to perform cleaning to aggregate totals at different levels like daily, weekly, monthly, and to parse nested structures like geoNetwork out of the JSON format. After the data is transformed, it is loaded into the targeted destination, such as the database and the organized data catalog. The catalog holds the appropriate data structure and schemas that support the analytical queries. In the analyze stage, a variety of tools and techniques can be used to extract useful information from data. The AWS Glue catalog is accessible using a web-based API that can be viewed in an easily accessible streamlit application. This makes the data ready for analysis to be done by multiple analysts using their choice of offline BI tools. (The completed analysis, reports, and visuals are stored in a separate S3 bucket.) SageMaker and Statistical tools allow for the following: 
- Describe characteristics of the dataset such as mean and standard deviation.
- Generate histograms to understand the distribution of values.
#
This solution allows ACME to scale its dataset to later include text data using other techniques such as counting the occurrence of each word in a text to get a sense of customers sentiment. It also allows for other technical aspects such as volume, variation, access, and security. The next step into migrating to the cloud is to adopt a machine learning solution. Adopting a ready-made ML model allows ACME to exploit current opportunities and focus first on their business requirements. In the future, the team can deliver an in-house solution. Up to this point, the following stages are complete:
- Data ingestion
- Data preparation
- Data segregation
#
We will now look at:
- Model Training/Fine-tuning
- Model evaluation
- Model deployment*
- Model monitoring*

 ![image](https://github.com/Tower-Babel/ACME_Targeted_Marketing/assets/123087201/ad677290-3706-43e3-8186-a05d3041d264)
 
# 
In the fine-tuning process, records from different datasets are joined and split into training validation and testing. Since we used a ready-made model, the model is fitted to ACME dataset to make sure that the model is not underfitted or overfitted. 
The model is evaluated using Root Mean Squared Error where y hat is the natural log of the predicted revenue for a customer and y is the natural log of the actual summed revenue value plus one. 
The model finds a small percentage of customers that produce most of the revenue and the marketing team will make an investment in their promotional strategy such as:
- Targeted email campaign: Send personalized coupon code.
- Exclusive Offers: Offer special deals on selected products that are not offered to others.
- Loyalty Program: Reward and incentive for spending the targeted amount.
- Feedback Survey: Polls offered to gather feedback that can refine the model.

For each visitor Id in the dataset, the model must predict the total revenue in the following format:
    ``fullVisitorID, PredictedRevenue
    0001_item_id, 0
    0002_item_id, 0
    0003_item_id, 0
    Etc…``

The small percentage of customers ID are given to the marketing team to make appropriate investments in promotional strategies to cross-sell to. 

## System Architecture

![1Monitoring_architecture drawio](https://github.com/Tower-Babel/ACME_Targeted_Marketing/assets/123087201/6c9480a4-6949-480b-9977-a67ef5d7cdc1)


