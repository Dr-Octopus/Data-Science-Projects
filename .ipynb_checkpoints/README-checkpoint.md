# Data-Science-Projects
You can find here some of my Data Science projects in different areas. A brief description is provided here, but each folder contain more details.
## 1. Computer Vision: Kaggle’s Deepfake Detection Challenge
 - The dataset provided in the [competition](https://www.kaggle.com/c/deepfake-detection-challenge/overview) consisted of around 20,000 real videos that were   used to generate 100,000 fake videos. All videos has a length of 10 seconds, and multiple people appeared in many videos.
- Computer vision is computationally expensive, and the large size of the dataset me makes it difficult to train models on the entire dataset. Therefore, a smaller dataset was generated, and it contained the majority of the unique people in the videos. A dimensionality reduction and clustering algorithms were used to find all the unique faces and build a smaller dataset.
- During the challenge I explored several Convolutional Neural Networks (CNN) architectures and used transfer learning to implement some of the best networks in the field.
- One of the challenges that I had to overcome was the time restriction to classify the videos. Each video needs to be classified in less than 8 seconds. However, facial detection is very time consuming. Therefore, I tackled this problem by running facial detection on every second, and then interpolate and extrapolate the locations to find the faces at every second of the video. This allowed me to find the faces at all the frames in 1.5 seconds only, leaving the rest of the time for classification.
- Unfortunately, I joined the competition at the last three weeks only, and I did not have enough time to reach the top of the leader board. However, the method that I was using, was also used by several teams that won in the top 5 positions.
## 2. Natural Language Processing: BBC articles summarization, topic modelling, and visualization
- Gather Articles: The first part uses beautifulsoup to extracts all the news articles currently on the BBC news.
- Article Summary: The article summary is generated based on a simple extractive method that ranks the sentences based on the words with the highest frequency. 
- Topic Modelling Using Latent Dirichlet Allocation (LDA): LDA topic modelling is used on all the articles.Top 10 words of the local and global topics are generated for each article.
## 3. Time-Series Forecasting: Avocado prices exploratory data analysis (EDA) and forecasting
- The avocado prices dataset is one of the popular datasets on Kaggle.
- Exploratory Data Analysis is first conducted to find the main features and patterns of the data with several statistical visualizations.
- ARIMA models and Facebook Prophet models were used to forecast the future prices and explore any trends and seasonality patterns in the data.
