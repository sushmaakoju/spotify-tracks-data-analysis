# spotify-tracks-data-analysis
## This is the repository for DTSC 5301 course, Data Science as a Field, University of Colorado Boulder.
### Dataset credits: https://www.kaggle.com/zaheenhamidani/ultimate-spotify-tracks-db
### About the Dataset features: https://www.kaggle.com/tomigelo/spotify-audio-features
### https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features

## The team consists of:
##### Sushma Akoju, Armana Anand, Avani Patil

## Dataset Description
#### Spotify Tracks Dataset is about playlist features and how they compare by genre or album/artist ids w.r.t popularity, acoustic ness, danceability, energy, instrumentals, key (musical chords) etc. Since all of us commonly listen to music, we found it interesting to explore various factors and their influence on playlists that become popular.

## About the features
#### It seems that Spotify has defined features based on various audio acoustic features such as Shimmer, pitch, tone, fundamental frequency, etc as well as musical acoustics. https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features. The audio features seem to be based on pitch ranges, harmonics, overtones of musical instruments along with known vocal quality metrics based on features such as jitter, shimmer, pitch, tone etc. Each of musical acoustics metrics, as well as voice acoustics metrics, are analyzed based on defined audio signal processing standards. The dataset attempts to bring metrics of musical acoustics and voice acoustics together to provide insights into how popularity compares, relates to the features such as energy.

- Understanding Audio features
    - Acousticness: 
    - Danceability: This is based on tempo, rhythm stability, beat strength, and overall regularity. On scale of 0 to 1, this metric suggests if the track is for dancing.
    - Energy: Indicates loudness of a track loudness, timbre, onset rate, and general entropy. Bach prelude seems to score low on this feature. The values are expected to be high for Heavy metal genre.
    - Instrumentalness: predicts if a track contains no vocals. Values above 0.5 indicate Instrumental tracks such as Classical music (example: soloist music).
    - Liveness: Detects presence of audience. This is indicator if this was recorded live. Higher value suggests this is a live recording.
    - Loudness: Loudness values are averaged across entire track and are measured in decibels (dB). Ranges -60 to 0. 
    - Speechiness: detects the presence of spoken words in a track. Measures the exclusivity of the speech over a scale of <= 1. ). Spoken content would give values closer to 1 and values >0.66 as well as values between 0.33 and 0.66 suggest musical tracks such as Rap song genre. Values below 0.33 indicate music and non-speech tracks.
    - Tempo: number of beats per minute (BPM). It is the speed or pace
        of a given track.
    - Valence: Defines the positiveness or negativeness of the track.
    - Mode: Mode indicates modality of the track such as minor or major scales - type of scale the melodic content is derived. Measured as 0 as Minor scale and 1 as Major scale.
    - Key: The track the key is played in. This is an Integer, 0 denotes C, 1 denotes C#. This follows Pitch class notation: <a  href="https://en.wikipedia.org/wiki/Pitch_class">https://en.wikipedia.org/wiki/Pitch_class</a>
- Types of <a href="https://en.wikipedia.org/wiki/Acoustic_music#Types_of_acoustic_instruments"> Acoustic instruments </a>

## Goal
#### We primarily focus and attempt to understand each of the features, their technical definitions cited here https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features . we would like to see how existing human notions about music fare against what data actually tells us about. For example, it has been widely popular that the C# chord is most popular in western music. We want to find out how the features contribute to popularity. 

### Clone the repository

```
git clone https://github.com/sushmaakoju/spotify-tracks-data-analysis.git
cd spotify-tracks-data-analysis
git status
```

### To upload changes to Github
```
cd spotify-tracks-data-analysis
git pull
git commit -m "one short summary of this change"
git push origin main

```

#### Data Analysis:
#### For raw github data content url: <a href="https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv">https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv</a>
##### Armana: Children's music genre has duplicated entries, general preporcessing and factorization of attributes, analysis and visualizations of attributes. https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/armana-anand
##### Avani's Data visualizations, analysis and Linear Regression Modelling: https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/avani-patil

##### My(sushma's) analysis on understanding musical and vocal acoustics and Data visualizations using <a href='https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html'>corrplot </a> library, and Linear regression with result analysis, Generalized Linear model, Random Forest regression, Permutation Importance and Feature importances analysis only w.r.t modelling and feature and permutation importances only: https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/sushma-akoju

##### Example songs, popularity scores: "My favorite things" song from "The Sound of music" movie which was very popular back in 1960s and still considered a classic is unfortunately has a popularity score of zero while a modern, contemporary version inspired from the same song and rewritten with different lyrics and named as "7 rings" by Ariana Grande, has a popularity score of 100.

### Github hosted pages
##### The R Github Markdown summary for this project is hosted at: https://sushmaakoju.github.io/spotify-tracks-data-analysis/







