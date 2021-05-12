# Spotify Recommender System

## Problem Statement
When engaging with content in our model world, corporations use recommender system to suggest future content we might like based on the attributes of the content. Be it movies or books that we may be interested in with the goal of keeping customer interested. However this may cause an echo chamber effect.

An extreme example of an echo chamber caused by recommender system is youtube's algorithm suggesting alt-right content which may lead to an individual developing extremist views. And this a problem of overtraining, because what is recommended is based on the data that is inputed to the system.

Spotify uses a common method for producing recommendations known as collaborative filtering which generates recommendations based on the combined preferences of the consumer requesting recommendations and those of other consumers. The underlying issue with this method is that song recommendations are based on the 'crowd'.

Furthermore, as the business model of Spotify is built in a way where artists are compensated by number of streams, the homogenisation of new music become more prevalent. Such as making songs more catchier and shorter.

The recommender system I would like to propose is for users to be recommended songs based on the 'DNA' of the music they have been listening to with the goal of potentially exposing the listener to songs form different genres and epochs. This is therefore a cluster or nearest neighbour recommendation system. This would broaden the horizon of music listeners and also bring attention to artists that create music as an artform as opposed to achieving the highest streaming numbers.

## Data Cleaning

While checking for duplicates, sometimes a duplicate can be remastered version of the first released song. By definition, remastering music is essentially improving on the quality of the original copy of a song or album. Removing flaws from the music, providing a cleaner, sharper and more refined listening experience whilst trying to bringing the music up to date with current standard. After remastering, certain attributes of the song would still generally remain the same, such as key, time signature, duration, tempo and speechiness. Nonetheless these duplicates, I would not remove them, as there are some music enthusiast that actually preferred 'non tampered' music.

Also, there are some artist that generally do not make explicit music, and would therefore not have duplicates of the same song where they only differ in explicitly. Removing duplicates by only keeping explicit songs would therefore result in removing many artists.

## Exploratory Data Analysis
![](./images/duration-of-music-decline-overtime.png)

![](./images/more-popular-as-song-duration-decrease.png)

Shorter duration in songs shows that artist are incentivised to make shorter songs for more plays as they are paid per stream. This may also reflect music listener's shortened attentions span.

Furthermore songs tend to be more popular, past the 50 mark, with shorter duration.

![](./images/loudness-increase-overtime.png)

Loudness, the inherent volume of the music itself, before any adjustments by the listener.

What this shows is dynamic range becomes much more restricted. As in, the contrast between the really soft stuff, and the really loud stuff shrinks, so the overall emotional impact of the music is reduced.

![](./images/variance-of-music-decreasing-over-time.png)

Key or pitch include details about harmony, melody, chords, and progressions – essentially how the notes were arranged and unfolded over the course of the song.

Data suggested that the variety of pitch progressions used has shrunk over the years. In other words, musicians are becoming less inventive and adventurous in how they get from one note or chord to the next, and instead seem to be relying more and more on the same sequences and patterns that others have used successfully in the past.

![](./images/music-released-in-january-the-highest.png)

Generally, the first two months of the year are a great time to release new music. Why? The market isn't as saturated as later on in the year, and the minds of listeners are open to new things.

## Clustering

### Clustering Genre Together

In this section, data_by_genres_df is used for clustering to see how the different genres would be clustered together based on their average song attributes, using different clustering methods.

By using this dataset, we can see the different kinds of genre you could expect from a given cluster.

### KMeans

Kmeans algorithm is an iterative algorithm that tries to partition the dataset into K pre-defined distinct non-overlapping subgroups (clusters) where each data point belongs to only one group. It tries to make the intra-cluster data points as similar as possible while also keeping the clusters as different (far) as possible.

Before deciding any value of K, we try the elbow method first.

![](./images/elbow-method.png)

From just using the elbow method, it suggest that 2 cluster is optimal. However just clustering 2973 genres into 2 clusters is not logical, I would therefore give my own K value or look into other clustering methods that makes more sense by just eyeballing it.

The K value that I had is 30. To visualise this on the high dimensional dataset, T-SNE projects it into lower dimensional space.

![](./images/k-mean30.png)

Visually, the segementation of the data does not appear to be the best. May have to reconsider the clustering algorithm or the number of cluster.

## Recommendations

Implicit
- or get implicit feedback on the number times a user skips recommended suggestion (not the most accurate as clicks can happen by accident)
- what is the ratio of songs added to the playlist against suggested
- the duration of the song you listen to
- how often the song is repeated provided its added into the playlist


Explicit
- have the user for explicit feedback whether they like the recommendation (perceived quality)

### Diferent types of Feature Selection/Extraction

- Using SVD (Singular Vector Decompostion) "Matrix Decomposition"
- Using PCA to select the most important variables

### Metrics

- Unsure if the metric is subject to the listener


### Building the Recommender System
- Naive and non personalised way by recreating the Collab Filtering as a baseline
- using distance to build a recommender system via clustered genres
- Using CNN as a recommender system
    - emulating this research paper https://www.sciencedirect.com/science/article/pii/S1877050919310646/pdf?md5=4f9a5242eb223b5c96c9ebf130855467&pid=1-s2.0-S1877050919310646-main.pd
- using cosine similarity

### Potential Limitations and Considerations

- kaggle dataset does not have user engagement and only genre metadata


 - Show why Collab filtering is not ideal due to the the cold start problem, also suggesting niche recommendation, requires reference from what may be a scare dataset. Generally why collab filtering would create an echo chamber because popularity of the music can be affected exogenous factors such as hype around the artist, your social group and so on.
