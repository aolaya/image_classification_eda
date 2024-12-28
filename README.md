# Image Classification Exploratory Data Analysis Summary
<p align="center">
    <!--MATPLOTLIB-->
      <img src="Images\matplotlib_logo.png"  width=15% alt="Matplotlib">
   <!--PLUS SIGN-->
          <img src="Images\plus_sign.svg" width=7% alt="Plus">
    <!--PANDAS-->
      <img src="Images\Pandas_logo.svg.png"  width=15% alt="Pandas">
   <!--PLUS SIGN-->
          <img src="Images\plus_sign.svg" width=7% alt="Plus">
    <!--OPENCV-->
      <img src="Images\OpenCV_Logo_with_text_svg_version.svg.png"  width=5% alt="OpenCV">
   <!--PLUS SIGN-->
          <img src="Images\plus_sign.svg" width=7% alt="Plus">
     <!--NUMPY-->
          <img src="Images\NumPy_logo_2020.svg.png" width=10% alt="Numpy">
   <!--PLUS SIGN-->
          <img src="Images\plus_sign.svg" width=7% alt="Plus">
     <!--SKIMAGE-->
          <img src="Images\skimage_logo.jpeg" width=10% alt="SKImage">

## About the Dataset

<p align="center">
    <!--FEATUREEXTRACIONS-->
      <img src="Images\sample_images.png"  width=90% alt="FeatureExtractions">
  
This dataset comprises of 25,000 images, each with a resolution of 150x150 pixels, divided into six categories: Buildings, Forest, Glacier, Mountain, Sea, and Street. The data is organized into separate zip files for training, testing, and prediction, with around 14,000 images in the training set, 3,000 in the test set, and 7,000 for prediction. In the training set, each feature has roughly 2,300 examples. In the test set, each feature has 500 examples.

## Preprocessing  
To prepare the dataset for analysis, several preprocessing steps were undertaken to standardize and optimize the input data. First, all images were resized to a uniform resolution of 150x150 pixels, ensuring consistent dimensions across the dataset. Next, pixel values were normalized by scaling them to a range between 0 and 1, a technique that improves numerical stability during training. Finally, a train-test split was applied, with training and test sets loaded separately to prevent data leakage. From the training set, a validation subset was further extracted to support hyperparameter tuning later on during the model training phase.

## Results
### HSV and HOG
<p align="center">
    <!--FEATUREEXTRACIONS-->
      <img src="Images\Screenshot 2024-12-20 115900.png"  width=70% alt="FeatureExtractions">

At first glance, we take a look at raw images and their corresponding contrast, HSV, and HOG features as seen above. Quickly, we can see distinct differentiators through the HSV and HOG feature vectors, otherwise, not obvious by just looking at the images alone.

For example in the second row, we compare & contrast histograms. Applying that to our classifications, buildings tend to skew right indicating high contrast perhaps due to the sky or window reflections, forests fall mid range indicating uniform textures without sharp contrasts, glaciers peak at higher intensity ranges perhaps picking up on the bright whites and blues seen, mountains tend to fall mid range similar to forest also indicating uniform texture although there seems to be slightly more brightness most likely due to bright skies, sea reflects patterns similar to glaciers reflecting the bright whites and blues usually observed, streets also reflect patterns similar to building however, a differentiation might involve low contrast as sunlight is usually blocked by aligned structures.

Building on that, the color histogram on the 3rd row comes in handy to distinguish between similar classifications mentioned: sea vs. glaciers and streets vs. buildings. Glaciers show more color diversity, low saturation, and high brightness compared to sea. Similarly, buildings have more color diversity compared to streets with low saturation.

Finally the last row helps differentiate between mountains vs. forests. Forests images show diffused and irregular edges indicating organic, non-linear textures of trees and foliage. While, mountain landscapes display sharp, angular edges corresponding to rocky terrains and slope. Overall, hog tends to aid in distinguishing between the images more successfully compared to hsv and contrast histograms. As Streets show slightly more variability due to mixed textures, while buildings retain grid-like consistency and so on.

Putting it all together, we selected the HSV and HOG features to feed into the machine learning models as they highlight details not easily noticeable beneath the surface of the images alone.

### PCA

<p align="center">
    <!--PCA-->
      <img src="Images\pca.png"  width=50% alt="PCA">
  
PCA appears to have limited utility for this dataset due to significant overlap between many categories. Urban categories like buildings and streets exhibit substantial overlap, reflecting their shared geometric and structural features, such as edges, lines, and muted tones. Natural categories like forests, mountains, and seas show broader dispersion, indicative of variability in natural textures and patterns. However, glaciers form a tighter cluster, suggesting that their consistent visual features—dominated by brightness and smooth textures—make them easier to separate.
Despite some broad distinctions, overlap persists between natural and urban categories, such as forests and mountains or seas and glaciers. These overlaps reflect shared characteristics like irregular textures, earthy tones, or reflective surfaces, which PCA’s linear nature struggles to distinguish effectively. This emphasizes the need for non-linear dimensionality reduction techniques or advanced feature extraction to better separate nuanced features.
While PCA provides an accessible summary of feature variance and relationships between categories, it highlights the challenges of achieving clear separability in this dataset. Techniques like t-SNE and texture-sensitive feature extraction are essential for improving classification performance and tackling the complexities of scene classification.


### T-SNE

<p align="center">
    <!--TSNE-->
      <img src="Images\tsne.png"  width=50% alt="t-SNE">
  
The t-SNE visualization offers a non-linear projection of the dataset, improving on PCA by better preserving local feature structure. While some categories, like forest, form tighter clusters due to their uniform brightness and smooth textures, others, such as buildings and streets, exhibit significant overlap. This overlap reflects shared structural features like edges and linear patterns, particularly within urban categories. Natural categories like forests, mountains, and seas display broader dispersion, with partial clustering for forests and overlap between mountains and glaciers, due to shared natural textures and color tones.

Compared to PCA, t-SNE provides better separation for certain categories, such as glaciers and forests, while still struggling with complex overlaps, particularly between urban and natural scenes. Categories with high variability, such as mountains and seas, remain more dispersed, highlighting the difficulty of isolating scenes with diverse features.

While t-SNE effectively reveals local relationships and achieves partial clustering, significant category overlap underscores the need for advanced feature engineering, such as texture- or context-sensitive methods, to further enhance separability and classification accuracy. This visualization demonstrates t-SNE’s strength in uncovering data structure while emphasizing its limitations for datasets with complex, overlapping features.

##### Source: https://www.kaggle.com/datasets/puneet6060/intel-image-classification
