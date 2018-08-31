+++
title = "Web Scraping Analysis Function"

date = 2018-07-20T00:00:00
lastmod = 2018-08-13T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = []

tags = ["Academic"]
summary = "Here is my web scraping analysis using Twitter API to perform sentiment analysis on cryptocurrency"

[header]
image = "twitter_analytics.jpg"
caption = "Image credit: [**Academic**](https://github.com/gcushen/hugo-academic/)"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-default.png"
caption = "Default"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-ocean.png"
caption = "Ocean"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-dark.png"
caption = "Dark"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-forest.png"
caption = "Default"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-coffee-playfair.png"
caption = "Coffee theme with Playfair font"

[[gallery_item]]
album = "1"
image = "https://raw.githubusercontent.com/gcushen/hugo-academic/master/images/theme-1950s.png"
caption = "1950s"
+++

I performed a sentiment analysis on each individual cryptocurrency using Twitter API to have a better understanding about the influence of social media on cryptocurrencies.


```{r, warning=FALSE, message= FALSE}
library(twitteR)
library(dplyr)
library(tm)
library(wordcloud)
library(tidytext)
library(tidyverse)
library(sqldf)
library(ggplot2)
library(ggthemes)
library(data.table)
library(gridExtra)

```

##### Built-funcrion for Web Scraping Analysis

I built a function to do some web-scraping analysis in order to facilitate the extraction of Twitter data.
```{r, warning=FALSE, message= FALSE}

setup_twitter_oauth(consumer_key, consumer_secret, access_token, access_token_secret)

twitter_scraping_data <- function(coin_name){
  
  coin_data = twitteR::searchTwitter(paste0("#",coin_name," -filter:retweets"),
                                 lang = "en", 
                                 n = 100, 
                                 since = '2017-08-01',
                                 until = as.character(as.Date(Sys.time())),
                                 retryOnRateLimit = 1)



d = twitteR::twListToDF(coin_data)
return(d)
  
}
```

##### Loading the dataset from CoinMarket
```{r, warning=FALSE, message= FALSE}
library(coinmarketcapr)
all_coins <- get_marketcap_ticker_all()
list_coin_names <- as.list(tolower(all_coins$name))
list_coin_names_20 <- list_coin_names[1:20]
```

##### Data Cleaning Part 1
```{r, warning=FALSE, message= FALSE}

datalist = list()

for (i in list_coin_names_20) {
  
  data = twitter_scraping_data(i)
  data$coin_name = i
  datalist[[i]] = data

}

big_data = do.call(rbind, datalist )


big_data_text <- big_data %>% select(text, coin_name)

big_data_text$text <- as.character(big_data_text$text)
str(big_data_text)


#applying to the big data

datalist_v2 <- list()

for (i in list_coin_names_20) {
  
 data = big_data_text %>%
    filter(coin_name == i) 
 
  data$text = stripWhitespace(data$text)
  
    data$text = gsub("[^[:alnum:][:space:]$]", "", data$text)
    
    data$text = tolower(data$text)
    data$text = removeWords(data$text, c(stopwords("english"),'ampamp','retweet','just','comment','amp','bitcoin','btc','xrp','eth','crypto','cryptocurrency', paste0(i), all_coins$symbol))

  data$coin_name = i
 datalist_v2[[i]] = data

}

big_data_clean = do.call(rbind, datalist_v2 )



```

##### Data Cleaning Part 2
```{r, warning=FALSE, message= FALSE}
datalist_v2 <- list()

for ( i in list_coin_names_20 ) {
  
  data <- big_data_clean %>% filter(coin_name == i) %>% select(text)
  data$text <- as.character(data$text)
  datatweets = VectorSource(data$text)
  datatweets = VCorpus(datatweets)
  
  datatweets_dtm<-DocumentTermMatrix(datatweets)
  datatweets_m<-as.matrix(datatweets_dtm)
  datatweets_wf<-colSums(datatweets_m)
  datatweets_wf<-sort(datatweets_wf,decreasing = TRUE)
  
  datatweets_wf$coin <- i
  datalist_v2[[i]] = datatweets_wf

}


#More data cleaning

data1 <- datalist_v2[["bitcoin"]]
data1 <- unlist(data1)
data1 <- as.data.frame(data1)
data1 <- cbind(words = rownames(data1), data1) 

rownames(data1) <- c()
data1 <- data1 %>%
  mutate(words_count = data1) %>%
  select(words, words_count)

```


##### Data Cleaning Part 3
```{r, warning=FALSE, message= FALSE}
#combining everything now

datalist_v3 <- list()

for ( i in list_coin_names_20) {
  
data1 <- datalist_v2[[i]]
data1 <- unlist(data1)
data1 <- as.data.frame(data1)
data1 <- cbind(words = rownames(data1), data1) 

rownames(data1) <- c()
data1 <- data1 %>%
  mutate(words_count = data1) %>%
  select(words, words_count)
  
data1$coin <- i
datalist_v3[[i]] = data1
  
}

big_data_clean_2 = do.call(rbind, datalist_v3 )

big_data_clean_2$words_count <- as.numeric(big_data_clean_2$words_count)
big_data_clean_2$words <- as.character(big_data_clean_2$words)

write.csv(big_data_clean_2, "big_data_clean_2.csv")
```

##### Data Cleaning Part 4
```{r}
datalist_v4 <- list()

for (i in list_coin_names_20) {
  data <- big_data_text %>% filter(coin_name == i) %>% select(text)
  
  data$text <- as.character(data$text)
  data <- data$text
  data <- as.tibble(data)
  data <- data %>% unnest_tokens(word, value)
  data$coin <- i
  datalist_v4[[i]] = data
}

big_data_clean_4 = do.call(rbind, datalist_v4 )


statement = paste0(" select sentiments.*,","DF",".word as SentimentWord from sentiments,","DF"," where sentiments.word = ","DF",".word ")

datalist_v5 <- list()

for (i in list_coin_names_20) {

DF <- big_data_clean_4 %>% filter(coin == i) %>% select(word)
  
statement = paste0(" select sentiments.*,","DF",".word as SentimentWord from sentiments,","DF"," where sentiments.word = ","DF",".word ")

data <- sqldf(statement)
data$coin <- i
datalist_v5[[i]] = data

}

big_data_clean_5 = do.call(rbind, datalist_v5 )
data_v5 <- big_data_clean_5[!duplicated(big_data_clean_5), ]
write.csv(data_v5, "data_crypto_sentiment.csv")

data_crypto_sentiment <- read.csv('data_crypto_sentiment.csv')


```


