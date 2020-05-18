# Kaggle’s Deepfake Detection Challenge
This Kaggle [competition](https://www.kaggle.com/c/deepfake-detection-challenge/overview) aimed to find the best algorithm for detecting deepfake videos. I participated in this competition at the last few weeks only. 
 - The dataset provided in the competition consisted of around 120,000 videos, which were split into 20,000 real videos that were used to generate 100,000 fake videos. All videos had a length of 10 seconds, and multiple people appeared in many videos.
 - Computer vision is computationally expensive, and the large size of the dataset makes it difficult to train models on the entire dataset. Therefore, a smaller dataset was generated, and I wanted it to contain the majority of the unique people in the videos. Thus, a dimensionality reduction and clustering algorithms were used to find all the unique faces and build a smaller dataset out of those. 
   - To perform the clustering of the videos, a single frame was taken from all the real videos. The main clustering code was based on this tutorial by [Adrian Rosebrock](https://www.pyimagesearch.com/2018/07/09/face-clustering-with-python/), which splits the procedure into two steps.
![Single frame samples taken from each video](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/Frame_samples.jpg)
**Figure1 : Single frame samples taken from each video.**
   - The first step is to detect the faces in all the images, and save the bounding box and facial encodings metadata to files. The facial encoding is 128-dimensional feature vector that quantifies the face, which is used in the clustering process. The notebook file for this step is (00_Cluster_encode.ipynb). 
![PCA of 20,000 facial encodings](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/PCA.png)
**Figure 2: PCA of 20,000 facial encodings.**
   - The second step was to actually perform the clustering analysis using DBSCAN from scikit-learn. The 20,000 facial encodings were first visualized through the Principal Component Analysis (PCA) dimensionality reduction algorithm. As expected, similar faces were closer to each other. Initially, the DBSCAN algorithm was used on its own, however, it was found that performing tSNE first improved the clustering results. Therefore, PCA, tSNE, and DBSCAN were all used to achieve the final clustering, the file for this step is ([01_Cluster_plot_all.ipynb](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/01_Cluster_plot_all.ipynb "01_Cluster_plot_all.ipynb")).
![tSNE of 20,000 facial encodings](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/tSNE.png)
**Figure 3: tSNE of 20,000 facial encodings.**
![Final clustering groups using DBSCAN](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/DBSCAN.png)
**Figure 4: Final clustering groups using DBSCAN.**

![Samples of nine clusters, each face is taken from an individual video. Other similar samples can be found in the Figures folder](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/Clustering_samples6.png)

**Figure 5: Samples of nine clusters, each face is taken from an individual video. Other similar samples can be found in the Figures folder.**

 - During the challenge I explored several Convolutional Neural Networks (CNN) architectures and used transfer learning to implement some of the best networks in the field. One of the main obstacles in this competition was the tendency of CNN to over-fit on the training data, and the networks may even memorize the faces. To overcome this, I decided to create masks of the altered regions and used Semantic Segmentation networks to detect those regions. This allows the network to focus only on the altered features, rather let the network decide on the features. The notebook that generates the segmentation masks is here [(02_Prepare_data.ipynb)](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/02_Prepare_data.ipynb "02_Prepare_data.ipynb").

![Samples of real, fake, and segmentation masks used to train the networks](https://github.com/Dr-Octopus/Data-Science-Projects/blob/master/Computer-Vision/Figures/Segmentation%20Mask.png)

**Figure 6: Samples of real, fake, and segmentation masks used to train the networks.**

 - Another challenge that I had to overcome was the time restriction to classify the videos. Each video needs to be classified in less than 8 seconds. However, facial detection on its own is very time consuming. Therefore, I tackled this problem by running facial detection on every second, and then I interpolated and extrapolated the face bounding box locations to find the faces at every frame of the video. This allowed me to find the faces at all the frames in 1.5 seconds only, leaving the rest of the time for classification.
 - Unfortunately, I joined the competition at the last three weeks only, and I did not have enough time to reach the top of the leader board. However, the method that I was using, was also used by several teams that won in the top 5 positions.