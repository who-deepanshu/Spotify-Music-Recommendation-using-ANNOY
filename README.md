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


