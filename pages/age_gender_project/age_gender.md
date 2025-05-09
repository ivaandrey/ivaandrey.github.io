## Age and Gender Estimation ##

**Age and gender estimation** from facial images is a fundamental task in computer vision with applications in security, marketing, human-computer interaction, and social analytics. The goal is to automatically predict a person's age and gender based on their facial features using deep convolutional neural networks (CNNs). The task is highly challenging due to variations in lighting, pose, facial expressions, face occlusions, as well as headwear and eyewear.

As part of my role in the company, I led the development of age and gender estimation networks. This project involved creating highly accurate models capable of estimating an individual's age and gender from images, leveraging state-of-the-art deep learning techniques. In addition to training and evaluating the models, one of my key responsibilities was the creation of diverse and high-quality datasets, ensuring that the models were trained on data representing real-world variations. I guided the entire process, from initial research and algorithm design to model training and deployment. The resulting models achieved an **accuracy of 94.9% [1-Class Off Accuracy (1CoA)](https://arxiv.org/abs/2108.08186) for age estimation and 99% accuracy for gender classification**, demonstrating their robustness and reliability in real-world applications.

---
<div style="text-align: center;">
  <img src="images/AgeGenderImage.jpg?raw=true" width="60%" height="60%">
</div>

+ **Face embeddings**: To address the problem of age and gender estimation, I decided to use facial embeddings as input for the models. Face embeddings are compact, high-dimensional feature representations extracted from a face image using deep learning models. Several pre-trained deep learning models can be used to extract facial embeddings. These models are designed to convert a face image into a fixed-size feature vector that captures facial identity. The [ArcFace (InsightFace)](https://insightface.ai/arcface?utm_source=chatgpt.com) network was used to create embeddings of faces. The model generates 512-dimensional embeddings, providing a good balance between feature richness and computational efficiency. ArcFace introduces Additive Angular Margin Loss (AAM), which enhances feature discrimination, ensuring that embeddings for different individuals are well-separated.
+ **Training Data**: Training an accurate age/gender estimation models requires diverse and well-labeled datasets. I used several publicly available datasets to train our age and gender estimation models, including: IMDB-WIKI, UTKFace, Adience, MORPH2, FG-NET. However, all these datasets are imbalanced in terms of age distribution, with fewer images of young children and very old individuals. We balanced the datasets by generating synthetic images for the underrepresented age groups to ensure more equitable representation. To balance the dataset, I utilized the GAN-based [SAM (Style-based Age Manipulation)](https://yuval-alaluf.github.io/SAM/) network. The SAM network is specifically designed for manipulating the age of individuals in images by leveraging a style-based generator architecture. By adjusting the latent code that controls the style of the image, SAM allows for the generation of faces at various stages of age progression or regression.

<div style="text-align: center;">
  <img src="images/SAM.png?raw=true" width="60%" height="60%">
</div>

+ **Network arcitecture** : A simple [MLP (Multilayer perceptron)](https://arxiv.org/abs/2108.08186) architecture was developed with skip connections to improve information flow and gradient propagation. The use of skip connections helps mitigate vanishing gradient issues and allows the network to learn both low-level and high-level features more effectively. This design ensures a balance between model complexity and computational efficiency, aligning with the requirement for negligible runtime while maintaining high accuracy. To ensure a stable and robust age estimation model, it was decided to train a classifier rather than a regressor. By using classification instead of regression, the model benefits from more stable predictions, avoiding small errors that could make continuous age estimation unreliable, better generalization, as age groups simplify the learning process. Instead of predicting a continuous age value, the model assigns each input to a specific age group. This classification-based approach helps mitigate the inherent challenges of age estimation, such as variations in facial appearance, lighting conditions, and dataset inconsistencies. To achieve this, the full age span from 0 to 90 years was divided into 18 discrete age groups, each covering a 5-year range.

<div style="text-align: center;">
  <img src="images/andrey_age.gif?raw=true"/>
</div>



