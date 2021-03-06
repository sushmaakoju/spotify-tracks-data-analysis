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
##### Data visualizations: Avani https://www.kaggle.com/zaheenhamidani/ultimate-spotify-tracks-db/download

### Visualization and modeling
#### Visualization:
#### use github rawuser content: <a href="https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv">https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv</a>
##### Using corrplot library:
##### My analysis and Data visualizations using <a href='https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html'>corrplot </a> library are: https://github.com/sushmaakoju/spotify-tracks-data-analysis/tree/main/sushma-akoju

- Understanding Audio features
    - Acousticness: 
    - Danceability: This is based on tempo, rhythm stability, beat strength, and overall regularity. On sclae of 0 to 1, this metric suggests if the track is for dancing.
    - Energy: Indicates loudness of a track loudness, timbre, onset rate, and general entropy. Bach prelude seems to score low on this feature. The values are expected to be high for Heavy metal genre.
    - Instrumentalness: predicts if a track contains no vocals. Values above 0.5 indicate Instrumental tracks such as Classical music (example: soloist music).
    - Liveness: Detects presence of audience. This is indicator if this was recorded live. Higher value suggests this is a live recording.
    - Loudness: Loudness values are averaged across entire track and are measured in decibels (dB). Ranges -60 to 0. 
    - Speechiness: detects the presence of spoken words in a track. Measures the exclusivity of the speech over a scale of <= 1. ). Spoken content would give values closer to 1 and values >0.66 as well as values between 0.33 and 0.66 suggest musical tracks such as Rap song genre. Values below 0.33 indicate music and non-speech tracks.
    - Tempo: number of beats per minute (BPM). It is the speed or pace of a given track.
    - Valence: Defines the positiveness or negativeness of the track.
    - Mode: Mode indicates modality of the track such as minor or major scales - type of scale the melodic content is derived. Measured as 0 as Minor scale and 1 as Major scale.
    - Key: The track the key is played in. This is an Integer, 0 denotes C, 1 denotes C#. This follows Pitch class notation: <a  href="https://en.wikipedia.org/wiki/Pitch_class">https://en.wikipedia.org/wiki/Pitch_class</a>
    - Duration_ms: Duration of track in milliseconds.
- Types of <a href="https://en.wikipedia.org/wiki/Acoustic_music#Types_of_acoustic_instruments"> Acoustic instruments </a>
- The features are extracted based on an custom Algorithm from The Echo Nest company. ()

---
##### title: "Spotify Tracks dataset"
##### author: "Sushma akoju"
##### date: "9/15/2021"
##### output: github_document
##### always_allow_html: yes
---

## Dataset Description
##### Spotify Tracks Dataset is about playlist features and how they compare by genre or album/artist ids w.r.t popularity, acoustic ness, danceability, energy, instrumentals, key (musical chords) etc. Since all of us commonly listen to music, we found it interesting to explore various factors and their influence on playlists that become popular.

## About the features
##### It seems that Spotify has defined features based on various audio acoustic features such as Shimmer, pitch, tone, fundamental frequency, etc as well as musical acoustics. https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features The audio features seem to be based on pitch ranges, harmonics, overtones of musical instruments along with known vocal quality metrics based on features such as jitter, shimmer, pitch, tone etc. Each musical acoustics, as well as voice acoustics, are analyzed based on defined audio signal processing standards.

## Goal
##### We primarily focus and attempt to understand each of the features, their technical definitions cited here https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features . we would like to see how existing human notions about music fare against what data actually tells us about. For example, it has been widely popular that the C# chord is most popular in western music. We want to find out how the features contribute to popularity. 

##### Example: "My favorite things" song from "The Sound of music" movie which was very popular back in 1960s and still considered a classic is unfortunately has a popularity score of zero while a modern, contemporary version inspired from the same song and rewritten with different lyrics and named as "7 rings" by Ariana Grande, has a popularity score of 100.

##### The following changes are from my analysis of Spotify Tracks dataset:

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, fig.width=30, fig.height=20)
options(scipen=999)

library(tidyverse)
library(readr)
library(dplyr)
library(ggplot2)
library(corrplot)
library(randomForest) # basic implementation
library(purrr)
library(corrr)
library(vtree)
library (reshape)
library(modelsummary)
library(gt)
library(kableExtra)
library(funModeling)
library(rpart)

library("permimp")
library("party", quietly=TRUE)

```


##### Get data from url to a Tibble.

```{r }
data_url <- "https://raw.githubusercontent.com/sushmaakoju/spotify-tracks-data-analysis/main/SpotifyFeatures.csv"
column_names <- c("genre","artist_name","track_name","track_id","popularity","acousticness","danceability","duration_ms","energy","instrumentalness","key","liveness","loudness","mode","speechiness","tempo","time_signature","valence")

spotifydf <- read_csv(data_url, show_col_types=FALSE)
head(spotifydf)
colSums(is.na(spotifydf))
head( spotifydf)
glimpse(spotifydf)
```

## Including Plots
##### Some genres are duplicated. (encoding mismatches).

```{r}
na.omit(spotifydf)
genres <- distinct(spotifydf, genre)$genre
genres
spotifydf$genre[spotifydf$genre=="Children's Music"] <- "Children???s Music"
spotifydf[!duplicated(spotifydf$track_id),]
genres <- distinct(spotifydf, genre)$genre
```

##### Convert character format columns: key and mode to numeric values. 

```{r}
unique(spotifydf$key)
unique(as.numeric(as.factor(spotifydf$key)))
spotifydf$key <- as.numeric(as.factor(spotifydf$key))

unique(spotifydf$mode)
unique(as.numeric(as.factor(spotifydf$mode)))
spotifydf$mode <- as.numeric(as.factor(spotifydf$mode))

```


##### Get all numeric columns from the dataframe.

```{r}
str(spotifydf)
columns <- colnames(spotifydf)
columns
numeric_columns <- unlist(lapply(spotifydf, is.numeric))
numeric_columns
numeric_spotifydf <- spotifydf[,numeric_columns]
colnames(numeric_spotifydf)
```

##### Use Corrr library to plot correlation based on feature groups.

##### Found this library more helpful to group into clusters for higher or similar correlation between features.

```{r}

corr_df <- correlate(numeric_spotifydf, quiet = TRUE)
corr_df
corr_df %>% 
  select(-term) %>% 
  map_dbl(~ mean(., na.rm = TRUE))

corr_df2 <- cor(numeric_spotifydf)
col3 = hcl.colors(10, "YlOrRd", rev = TRUE)
corr1 <- corrplot(corr_df2, col=col3, method = 'number') 

corrplot(corr_df2,  order = 'hclust', addrect = 2)
corrplot(corr_df2/2, col.lim=c(-0.5, 0.5))
```


##### There is a high correlation between energy and loudness features and similarly there is a second highest correlation between valence and danceability where valence is positiveness or negativeness of a track defined by (cheerful vs sad, depressive tune, lyrics)

##### For each feature, plot grouping w.r.t Popularity.

```{r}

genres_df <- spotifydf %>%
   select(popularity, genre)%>%
    count(popularity, genre)
by_genres <- spotifydf %>% group_by(genre, popularity)
by_genres %>% summarise(
  popularity = mean(popularity),
)
by_genre <- by_genres %>% summarise(n = n())
by_genre %>% summarise(n = sum(n)) %>% filter(n>0)
#vtree(genres_df, "genre")
colnames(by_genre)

ggplot(genres_df)+
  geom_point(aes(x = genre, y= n))

genres_df %>% ggplot(aes(x = genre, y= n))+
  geom_line(aes(color = "genre")) 

ggplot(data=by_genre,aes(x = genre, y = n, fill=genre)) +
  geom_bar(stat="identity", width=0.5,  position=position_dodge())+
coord_flip()+
    labs(title = "Spotify tracks by Genre in US", y= NULL)
```

##### Group by Genres and select all features except text based features.

```{r}

genres_df <- spotifydf %>%
  select(-c(artist_name, track_name, track_id, time_signature, key))

```


##### Each of features do seem to have different types of density, suggesting distributions are different from each other. It would have been nice if some normalization technique or re-sampling of features was done. But in the interest of time, we could not do this. From the above density plots, it would be reaosnable to find some kind of normalization between feature data.

```{r}
spotify_summary <- datasummary_skim(numeric_spotifydf)
spotify_summary
```

##### Plot the density distributions of each of features.

```{r}
spotify_histograms <- numeric_spotifydf[,-c(4)]
plot_num(spotify_histograms)

ggplot(spotifydf, aes(popularity)) +
  geom_density()
ggplot(spotifydf, aes(energy)) +
  geom_density()
ggplot(spotifydf, aes(danceability)) +
  geom_density()
ggplot(spotifydf, aes(key)) +
  geom_density()
```

## Sushma Akoju: 

##### Check linear fit between all features vs popularity
##### This is multiple regression since we have multiple predictors vs one response variable.

##### We find a linear fit for y = [popularity] and X = [ acousticness, danceability, duration_ms, energy, instrumentalness, liveness, loudness, speechiness, tempo, valence] to check model fit.

```{r}

lmfit = lm(popularity ~ acousticness + danceability + duration_ms +energy + instrumentalness + liveness + loudness + speechiness + tempo + valence, numeric_spotifydf )
summary(lmfit)
plot(lmfit)
```

## Sushma Akoju: 

##### The summary of linear fit suggests that R-squared value is 0.2339 which is not significant enough to explain how much percentage of data fits linearly. Standard error is 15.92 suggests this is 15.92 standard deviations of the residuals away from true regression fit. The p-value of less than 0.01 suggests that null hypothesis that predictors and response variables are not related can be rejected. Hence observed values of response variable are no better than predicted values, by a chance. However since this is a multiple linear regression, F-statistic may also be relevant here since it checks if atleast one of the predictors' coefficients is non-zero. F-statistic = (SSR/SSE) = (Sum of squares regression) / (sum of squares error) -> is the ratio of variance explained / varinace that cannot be explained. The standard errors suggest that about ~75% of variance in data cannot be explained. P(> |t|) for each of features also suggests null hypothesis that there is no relation between predictors and response variable - must be rejected.

## checking coefficients

```{r}
coefficients(lmfit)
```

## Above coefficients seems to show


```{r}

lmfit2 = lm(popularity ~ acousticness + danceability +energy + instrumentalness + liveness + loudness + speechiness + tempo + valence + key+mode+(energy * loudness) + (valence * danceability) , numeric_spotifydf )
summary(lmfit2)
```

##### The summary of linear fit suggests that R-squared value is 0.2392 which should be significant enough to explain how much percentage of data fits linearly. Standard error is 15.92 suggests this is 15.92 standard deviations of the residuals away from true regression fit. The p-value of less than 0.01 suggests that null hypothesis that predictors and response variables are not related can be rejected. Hence observed values of response variable are no better than predicted values, by a chance. However since this is a multiple linear regression, F-statistic may also be relevant here since it checks if atleast one of the predictors' coefficients is non-zero. F-statistic = (SSR/SSE) = (Sum of squares regression) / (sum of squares error) -> is the ratio of variance explained / varinace that cannot be explained. The standard errors suggest that about ~75% of variance in data cannot be explained. P(> |t|) for each of features also suggests null hypothesis that there is no relation between predictors and response variable - must be rejected. From p(>|t|) = 0.08 for valence, seems to indicate null hypothesis true for valence and popularity score suggesting that valence has no influence on popularity score.

```{r}
anova(lmfit2)
```


```{r}
plot(lmfit2)
```




##### get model summary for Linear regression and Generalized Linear regression with Gaussian.

```{r}
models <- list(
  "OLS"     = lmfit2,
  "GLM" = glm(popularity ~ acousticness + danceability +energy + instrumentalness + liveness + loudness + speechiness + tempo + valence + key+mode+(energy * loudness) + (valence * danceability) , data = numeric_spotifydf , family = gaussian)
)
modelsummary(models,
             fmt = 1,
               estimate  = c(
                "{estimate} ({std.error})",
                "{estimate} [{conf.low}, {conf.high}]"),
               statistic = NULL,
              coef_omit = "Intercept",
             output = "table1.png")


```

##### Get standard errors, statistics and p-values for each of models.

```{r}
modelsummary(models,gof_omit = ".*",
               statistic = c("conf.int",
                           "s.e. = {std.error}", 
                           "t = {statistic}",
                           "p = {p.value}"),
             output = "table2.png")
```

##### taking linear regression fit analysis further, using model summary package we are able to compare how features fit in comparison between linear regression as well as Gaussian Generalized Linear regression fit. There is no change in P-values or null hypothesis analysis. However, individual feature's standard errors seems significant and are very low. This suggests that linear regression (generalized or OLS) seem to be overfitted.

##### Random Forest Regression fit by train and test split.
### Create train and test sets

```{r}
train = sample(1:nrow(numeric_spotifydf), 300)
rf.spotify = randomForest(popularity~., data = numeric_spotifydf, subset = train)
rf.spotify
```

##### In case of Random Forest regression, number of trees are 500 with 4 variables at each split. as well the MSR is 273.81 and explained variance is still low 27.88 % of variance explained.
The following plot suggests that 50 trees or so is enough to fit the model with RFR.

```{r}
plot(rf.spotify)

```

##### For each variables 1 to 17 of features, find Out-of-bag and test errors for each fit.

```{r}
oob.err = double(17)
test.err = double(17)
for(mtry in 1:17){
    fit = randomForest(popularity~., data = numeric_spotifydf, subset=train, mtry=mtry, ntree = 350)
      oob.err[mtry] = fit$mse[350]
      pred = predict(fit, numeric_spotifydf[-train,])
      test.err[mtry] = with(numeric_spotifydf[-train,], mean( (popularity-pred)^2 ))
}

```

##### Random Forest Regression Trees 17*350 trees with MSE for OOB and Test errors

```{r}
matplot(1:mtry, cbind(test.err, oob.err), pch = 23, col = c("red", "blue"), type = "b", ylab="Mean Squared Error", lwd=6)
legend("topright", legend = c("OOB", "Test"), pch = 23, col = c("red", "blue"))

```

##### The above plot suggests that Out-Of-Bag error estimates (red colored curve) is very far apart from test error estimates. There is no correlation between OOB and test errors. Errors never really tends to minimize as the number of features increase during training.

```{r}
oob.err 
test.err
```

##### Basic Random Forest on all features

```{r}
rf.spotify1 = randomForest(popularity~., data = numeric_spotifydf, subset = train, importance = TRUE)
rf.spotify1
summary(rf.spotify1)
```

```{r}
plot(rf.spotify1)
```


##### In case of Random Forest regression, number of trees are 500 with 4 variables at each split. as well the MSR is 268 and explained variance is still low 29.36 % of variance explained.

##### Use Random forest to find Variance based Feature Importances.

```{r}
rf.spotify1$importance
rf.spotify1$importanceSD
```

##### Plot the Feature importances from Random Forest Regression for each feature.

```{r}
create_rfplot <- function(rf, type){
  
  imp <- importance(rf, type = type, scale = F)
  
  featureImportance <- data.frame(Feature = row.names(imp), Importance = imp[,1])
  
  p <- ggplot(featureImportance, aes(x = reorder(Feature, Importance), y = Importance)) +
       geom_bar(stat = "identity", fill = featureImportance$Importance, width = 0.65) +
       coord_flip() + 
       theme_light(base_size = 25) +
       theme(axis.title.x = element_text(size = 20, color = "black"),
             axis.title.y = element_blank(),
             axis.text.x  = element_text(size = 20, color = "black"),
             axis.text.y  = element_text(size = 20, color = "black")) 
  return(p)
}
create_rfplot(rf.spotify1, type = 2)

```


##### The Random Forest Regression Feature importances suggest that duration is the most important feature of the response variable i.e Popularity score.

```{r}
data.frame(Feature = row.names(rf.spotify1$importance), Importance = rf.spotify1$importance[,1])
```

##### To do permutation Importance to compare Feature importances with that of Feature Importances from Random Forest regression's variance based importance, we need forest and inbag values to be available in RFR forest object so Permutation-based analysis over repeated samples of all-features-except-one is done based on available statistical information. This makes Permutation Importance more relevant. The Permutation Importance done here is also conditional since we observe multi-collinearity between predictors/independent features themselves. Conditional Permutation importance more relevant in this case since finding accuracy when correlation threshold is (suggested > 0.2) which is true in this case. We have multiple features having correlation > 0.2 suggesting Conditional Permutation Importance as more appropriate method to find importance of a feature's relation to response variable.

```{r}
rf.spotify2 = randomForest(popularity~., data = numeric_spotifydf, subset = train, replace = FALSE, nodesize = 7, keep.forest = TRUE, keep.inbag = TRUE)
rf.spotify2
permimp <- permimp(rf.spotify2, conditional = TRUE, progressBar = FALSE, do_check=FALSE)
```

##### Permutation Importances are calculated by repeated bagging, bootstrapping and sampling from Random Forest Regression fit to derive importance of a feature based on change in error (positive or negative or none). If there was no change in error in absence of a feature, that feature is considered not important for observed values of reponse variable.


```{r}
permimp$values
```

```{r}
ggplot(as.data.frame(permimp$values), aes(x = reorder(names(permimp$values)
, as.numeric(permimp$values)), y = as.numeric(permimp$values))) +
       geom_bar(stat = "identity", fill = as.factor(seq(0,11)), width = 0.65) +
       coord_flip() + 
       theme_light(base_size = 25) +
       theme(axis.title.x = element_text(size = 20, color = "black"),
             axis.title.y = element_blank(),
             axis.text.x  = element_text(size = 20, color = "black"),
             axis.text.y  = element_text(size = 20, color = "black"))+xlab("Features")+ylab("Importance")
```


##### Lastly, we see that on the contrary, acousticness has no influence over popularity score. However, duration, instrumentalness, loudness, valence seem to have good influence over response variable.

##### Finally, we think given the number of tracks, we can use most statsitically important features to train and test regression fit using cross validation and epochs. Further we would like to conduct tests on a randomly generated date from the model fit. We further would like to explore, as a future work, to find regression or models that better  fit multi-collinear features while also finding some better techniques to normalize each of feature-wise distributions. The additional information about musical and vocal acoustics and the pattern in which the acoustic signals themselves relate to the popularity score will be helpful.




