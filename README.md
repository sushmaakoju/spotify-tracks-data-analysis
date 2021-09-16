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
#### It seems that Spotify has defined features based on various audio acoustic features such as Shimmer, pitch, tone, fundamental frequency, etc as well as musical acoustics. https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features The audio features seem to be based on pitch ranges, harmonics, overtones of musical instruments along with known vocal quality metrics based on features such as jitter, shimmer, pitch, tone etc. Each musical acoustics, as well as voice acoustics, are analyzed based on defined audio signal processing standards. The dataset attempts to bring metrics of musical acoustics and voice acoustics together to provide insights into how popularity compares, relates to the features.

## Goal
#### We primarily focus and attempt to understand each of the features, their technical definitions cited here https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features . we would like to see how existing human notions about music fare against what data actually tells us about. For example, it has been widely popular that the C# chord is most popular in western music. We want to find out how the features contribute to popularity. 

### Clone the repository

```
git clone https://github.com/sushmaakoju/spotify-tracks-data-analysis.git
cd spotify-tracks-data-analysis
git status
```

#### Data Analysis:
#### For raw github data content url: <a href="https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv">https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv</a>
##### Armana: Children's music genre has duplicated entries, https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/armana-anand
##### Avani's Data visualizations: https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/avani-patil
##### My(sushma's) Data visualizations using <a href='https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html'>corrplot </a> library are: https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/sushma-akoju
