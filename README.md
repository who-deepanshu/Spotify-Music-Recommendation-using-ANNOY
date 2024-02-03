# Spotify Music Recomendation System
- **ANNOY (Approximate Nearest Neighbors Oh Yeah!)** is not specifically related to Spotify itself, but it is a library that can be used for efficient nearest neighbors search in high-dimensional spaces. Nearest neighbors search is a common task in recommendation systems, including those used by music streaming services like Spotify.


# Let's walk through this :
**Dataset -** Used google research [Audio data](https://research.google.com/audioset/download.html). Which offer the AudioSet dataset for download in two formats:

- Text (csv) files describing, for each segment, the YouTube video ID, start time, end time, and one or more labels.
- 128-dimensional audio features extracted at 1Hz. The audio features were extracted using a VGG-inspired acoustic model described in Hershey et. al., trained on a preliminary version of YouTube-8M. The features were PCA-ed and quantized to be compatible with the audio features provided with YouTube-8M. 


# Embedding Generation:
- **IBM Code Model Asset Exchange** - It's a pre-build model for Audio Embedding purpose which embedds data in a lower-dimensional space, and audio embeddings can be particularly useful for tasks like audio similarity or recommendation systems.


# Demo.ipynb :
- In this file, **IBM Code Model Asset Exchange** is used to train the model on our dataset of music and get it in embeddings format for finding cosine similarity whenever a new music sample is input it will return it in vectors.


# AudioSet Processing.ipynb :
- Here, we are extracting the related features from the each sample in the dataset and storing them in the **JSON** format.
- These features are - 
    - Label
    - Id
    - Starting time
    - End time
    - Data(audio embedded)


# Recommendor using ANNOY.ipynb :
- At last, we used **ANNOY** to predict top 10 nearest vectors which are related to the input sample.
- The **JSON** file in which data is stored in the vector embedded form.
- **AnnoyIndex** is used to build an index of vectors and quickly retrieve the approximate nearest neighbors of a query vector.
- So, we pass all of our data through **AnnoyIndex** which create a matrix representation of our data and whenever new sample is introduced then its nearest neighbors can be calculated by finding **cosine similarity** to that vectors.


# How ANNOY works ?
**ANNOY** uses tree data structure to store vector space.It takes two random points in a vector space then split the space into two by doing a perpendicular to these two points and it continues to do it till we finds k neighbours.
<p align="center">
  <img src="https://github.com/who-deepanshu/Spotify-Music-Recommendation-using-ANNOY/assets/129099978/f066fe6c-e507-4dd4-bc82-bcaf45211a2e" width="600" height="370"</img>
</p>  

The division between two points result as a split in a tree.
<p align="center">
  <img src="https://github.com/who-deepanshu/Spotify-Music-Recommendation-using-ANNOY/assets/129099978/d81e39c2-e8e9-4b09-8d29-fcb9c325b0f4" width="600" height="370"</img>
</p>

These two points are so close in hyperplane which may make us split the vector into two even if they are so close. Thus, instead of building one tree it builds many trees and then take union of the neighbours and removes duplicates. The left ones are returned as top most nearst neighbours.
<p align="center">
  <img src="https://github.com/who-deepanshu/Spotify-Music-Recommendation-using-ANNOY/assets/129099978/abdd8e59-8695-45d2-9c1d-2b4a68c89525" width="600" height="370"</img>
</p>

**ANNOY** simply builds random tree. At every intermediate node in the tree, a random hyperplane is chosen, which divides the space into two subspaces. This hyperplane is chosen by sampling two points from the subset and taking the hyperplane equidistant from them.We do this k times so that we get a forest of trees. k has to be tuned to your need, by looking at what tradeoff you have between precision and performance.
