
# Visualizing Movie Reviews in Word Cloud

Samrat Halder and Hariz Johnson


## IMDB Reviews
We first scrape all the movie reviews from IMDB 

```r
library(rvest)
library(xml2)
library(plyr)
result <- c()
ID <- 4154796
movie_IMDb <- read_html(paste0("https://www.imdb.com/title/tt",ID,"/reviews?ref_=tt_urv"))
reviews <- movie_IMDb %>% html_nodes("#pagecontent") %>% html_nodes("div.content") %>% html_text()
#perfrom data cleaning on user reviews
reviews <- gsub("\r?\n|\r", " ", reviews) 
reviews <- tolower(gsub("[^[:alnum:] ]", " ", reviews))
write.csv(reviews, paste0(getwd(),"/resources/wordcloud_sentiment/reviews.csv"))
head(reviews)
```

```
## [1] "                 there is no way that i could describe my emotions for this movie  i m totally speechless  i haven t laughed  even cried  this much in marvel movie or even in any movie  i m fully on my emotion  there are so many tears of joy and loss  amazing story  the acting is outstanding  epic action  great cgi  the best storytelling ever told in a superhero movie  amazing performance  i love it more than 3000 happiness  sadness  pure joy  excitement    i m gonna miss this moment in my whole life because let s face it  it s been awhile movies can bring such a big enthusiasm like this it is such an experience you ll gonna remember it forever  people are clapping  laughing  crying  full of a state emotion  it s 3 hours long but it went by like a finger snapping by thanos  and now i m thinking i m actually in quantum realm because it felt like 5 seconds  even though you know where the story is gonna bring you because it s still a  superhero movie  but it left me speechless  it s not just a superhero movie  it s more than that   spoiler alert  even some characters that you didn t like before  you will love them in this movie  like captain marvel  i didn t like her before in her own movie but in endgame they showed how powerful  how strong and how capable she really is  and now i kinda love her  but marvel should really be careful of her line though  i didn t like some of her line like  i m the strongest  and  you didn t win because before you didn t have me  duh  also not gonna forget hawkeye  to be honest  in avengers i really didn t like hawkeye because he s just a  guy  with an arrow and just randomly showed up in any scene but actually he s character is so badass  everything that we need  what we want is here also i don t get it why some people can not accept that thor is fat or treat him like a joke  i mean  this movie might be trying to give us a message about no matter what  shape  are you  you can be a hero and save the world  to be honest  i like what they did to thor  that man is depressed and taking the most responsible after he missed the shot to kill thanos in infinity war  even though he already did killed him but it s not gonna bring back his people of asgard  also he s god of thunder for god sake  he could slap his stomach with thunder and got his abs back i m so happy too for captain america  finally he could do his dance with peggy and i didn t expected that we could see the fight between captain america with his own self  also when tony met his father really warm my heart  and we can see the  real life  jarvis   i didn t expected that too when the whole superhero arrived it is so epic  the whole person in theater are screaming and shocked  gives me a goosebumps and still left me speechless this movie is absolute perfection  the ending of this movie is we and the characters deserved  it gives a perfect balance for all these past 10 years  epic and perfect ending  i was not disappointed at all  this movie was completely emotional and visually stunning  now i get it why the russo brothers told us to do a marvel movie marathon before watching endgame because this movie had everything to accomplish what left behind before all of this ready or not  whatever it takes go watch it for yourself                                       4 191 out of 6 336 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "                                                                      
## [2] "                 endgame is a great popcorn action movie to  finish  a saga of popcorn action movies  this isn t serious entertainment and shouldn t be considered as such  and it reminds me of how george lucas made star wars as an homage to the cheap serials like flash gordon  especially as comic sourced material  this is what the mcu is  some part of me is actually a bit pained to like it as much as i do  given that it is just playing on base emotions to make money for a massive conglomerate like disney but    what a great way to end several major storylines that they invested in over the past 11 years  for people who have watched the saga  i feel like this is just the cherry on the top  my only complaint is something that you can t really get away from in superhero stories  the character  powers  are totally inconsistent from scene to scene  and movie to movie  this is a trope that there s no getting away from  because if characters like captain marvel  thor  scarlet witch  and hulk were always as powerful as they show flashes of  then the story wouldn t even be a thing  any one of them could destroy thanos in the blink of an eye  and have done similar feats in other stories  and even in other scenes within a given story   that they sometimes  reduce  their power to a lower level  without an explained mechanism  is pretty laughable  and makes some parts of the story a bit nonsensical  yes  this constant ex machina is needed to maintain the drama and keep the plot going  but it s still something that takes me out of the story what i really love about this movie  and the saga as a whole  is how good it is at developing the actual characters and their relationships  there are some similarities  but nobody is the same  and most of the arcs are believable  thor s story  and apparent ptsd  is to me the best done  but all of the majors  and some of the minors  are almost as good  i believed them  and for a popcorn action movie saga based on a comic series  i think that s a pretty high compliment                                       256 out of 417 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               
## [3] "                 after avengers infinity war  we waited for the avengers endgame  we wondered how the story would go on  how our heroes would turn back  what would be the end of thanos  many theories related to this have been put forward  avengers endgame was undoubtedly the most anticipated film of recent years  normally  the higher the expectation  the higher the probability of disappointment  but this is not the case for endgame  whatever you re expecting  you find much more in the film  this means that the biggest concern about the film has disappeared on the other hand  another comparison comes up  is endgame more successful than infinity war  we can comfortably say it avengers infinity war is just the beginning of the story  endgame was the finale of the story  so we shouldn t think of these two films as two separate stories  there is only one story divided into two parts avengers endgame is  above all  a great homage to the ten year history of the marvel cinematic universe  the story highlights the original avengers team  iron man  captain america  thor  hulk  black widow and hawkeye are at the center of events  no character comes in front of them  of course there are many characters that play an important role in the story outside the original avengers team  everyone s concern was that captain marvel  who was included in the marvel world  overshadowed other heroes  we can say that this certainly did not happen  what is important in this struggle is not how strong you are  but how good you are  this comes to the fore in all areas  it gives good message about being a hero and a family of course  avengers endgame has some critical aspects  for example  is the three hour period necessary in terms of the story  it can be discussed  the head of the story moves much slower than the rest  it also drags the heroes into an emotional predicament  then the tempo is rising and the heavy scenes we are watching are getting more meaningful  the last 45 minutes of the movie is fully action packed  but the last 45 minutes goes so fast that you don t even realize it  action and battle scenes are really successful  there is not even a slight distress about visual effects  there are also slight logic errors in the film  but in general the story is so successful that these details become meaningless and insignificant after a certain point lastly  avengers endgame doesn t have a movie end scene  because after the film s final  there is no need for another scene  the marvel legend stan lee appears with a small stage  but this is the last surprise scene in the marvel cinematic universe  moreover  there is no clue about marvel s future  this makes us wonder more about spider man  far from home  10 10                                      1 916 out of 3 311 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
## [4] "                 i have to say  my first reaction walking out of the cinema was that it was great  probably an 8 10  you know there s so much fan service in this movie and i particularly loved the  i can do this all day  ca line from one ca to another  it was almost toy story 2  enlightened buzz to naive buzz banter i loved clever hulk  found thor hilarious  though a bit annoying at times  and loved the references to past movies  cap swinging mjollnir around was beautiful the deaths in this movie were also pretty surprising but i agree with some of the more balanced reviews in here that it was bizarre that so much time was spent on hawkeye   does anyone really care about him  not really killing off black widow was a surprising touch  but i  like many others  probably felt more of an emotional reaction to banner s relationship with her and not hawkeye  because no one actually cares about him   renner  as an actor  just doesn t cut it much  unfortunately the real problem with end game  is the time travel  i don t know why any movie franchise would ever want to deal with time travel knowing how much grief it creates  sure they try to explain everything with their hilarious conversation about movies  but in the end  there are just too many questions left at the end of the day  particularly when they already try to explain it through the ancient one the most glaring one of these is  if they change the past  they re changing another timeline  so how selfish is that  if tony stark snaps his fingers and kills thanos  what happens to that original timeline  if he sent thanos and everyone back  how does he magically know not to send gamora back who is now stuck in 2023   and so does that mean 2014 quill never meets gamora    what the hell  essentially erasing the entire 2014 gotg franchise in that universe  if captain america goes back in time  he will inevitably change history in some way or another  so that is another timeline  right  so while everyone else s timeline is meant to stay the same in the present  as said by stark  how does cap end up sitting by the same lake as everyone else there are also way too many questions about new timelines created   but perhaps that is intentional  such as the loki tv show  but this is why i hate it when they bring time travel into any movie and just add stuff to it to make it wrap up nicely in their own universe also  don t get me started on how impossibly strong thanos suddenly is without an infinity gauntlet  even with the ig he couldn t stop thor s stormbringer  but now without the ig can easily defeat thor with stormbringer and mjollnir  iron man and cap    how convenient i also think marvel made a serious mistake creating captain marvel  how is she brought in as a convenient deus ex machina and yet doesn t really stick around to show off all her abilities  and she can t even defeat thanos single handedly  pfft  that was rich  she can barely prevent thanos from snapping his fingers  yet in infinity war  cap was able to actually hold off his hand too  bizarre parallels so okay  sure  it was enjoyable to watch  but i just feel that there are too many plot inconsistencies creeping into end game  there should have been better ways to get the infinity stones back  and i think someone stupid just thought time travel was the best way to do it                                        2 667 out of 4 645 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "
## [5] "                 this is getting a 10 10 mostly because how it doesnt flop on its head ending a 22 movie long plot  is this the best marvel movie  no not even close  is this as good as infinity war  no  me 2 months ago would say it is but me now would say other wise  but simply for the experience of seeing the first iron man in theaters when i was 8 to now me as 19 and making me cry it is easily a 10 10 due to it being like no other experience  if it wasnt an ending to a 22 movie long era than mayhe my score would reflect like an 8 or a 7  but due to it being what it is i am willing to bump it up  it is still better than like 15 marvel movies  it s still up there for one of their stronger movies  it s not as good as infinity war and winter soldier is still my favorite marvel movie not counting spiderman movies  tldr  its simply unlike any experience in film yet  having a movie end a 22 movie long story and not flop on its face  usually movies cant finish a 3 movie long story without flopping  yet this movie managed to do it with a 22 movie long story  it isnt the best marvel movie  far from it  i would argue that infinity war is a much better movie  but i would say that this is my 2nd favorite avengers movie                                      206 out of 337 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
## [6] "                 where to start     this is such a bad movie that i am so disappointed with marvel  can t believe critics who are rating such movies so high  its very clear that we cannot go by what critics say  good movies are bad and bad movies are good                                        36 out of 52 found this helpful                                                       was this review helpful   sign in to vote                                                   permalink                              "
```
## Cleaning the data!
In this part first we clean the data using standard text mining techniques eg. removing redundant characters, stop words, stemming etc


```r
library(tm)
library(plyr)
library(stringr)
library(wordcloud)
library(RColorBrewer)

removeURL <- function(x) {
  gsub("http[[:alnum:]]*", "", x)
}
removelongWORDS <- function(x) {
  gsub("\\b[[:alpha:]]{15,}\\b", "", x, perl=FALSE)
}
removeCharacters <-function (x, characters)  {
  gsub(sprintf("(*UCP)(%s)", paste(characters, collapse = "|")), "", x, perl = FALSE)
}
reviews <- read.csv(paste0(getwd(),"/resources/wordcloud_sentiment/reviews.csv"), row.names = NULL)
dataset <- reviews$x
dataset <- str_replace_all(dataset, "[^[:alnum:]]", " ")
CorpusObj<- VectorSource(dataset)
CorpusObj<- Corpus(CorpusObj)
CorpusObj <- tm_map(CorpusObj, removelongWORDS)
CorpusObj <- tm_map(CorpusObj, removeURL)
CorpusObj <- tm_map(CorpusObj, removePunctuation)
CorpusObj <- tm_map(CorpusObj, removeNumbers) 
CorpusObj <- tm_map(CorpusObj, removeCharacters, c("\uf0b7","\uf0a0"))
CorpusObj <- tm_map(CorpusObj, tolower)
CorpusObj <- tm_map(CorpusObj, stemDocument, language = "english") 
CorpusObj <- tm_map(CorpusObj, removeWords, 
                    c(stopwords("english"), "text show-more__control", "movi",
                      "like","vote", "also","review", "permalink", "help", "stori","charact")) 
CorpusObj<-tm_map(CorpusObj,stripWhitespace)
CorpusObj.tdm <- TermDocumentMatrix(CorpusObj, control = list(minWordLength = 3)) 
freqr <- rowSums(as.matrix(CorpusObj.tdm))
CorpusObj.tdm.sp <- removeSparseTerms(CorpusObj.tdm, sparse=0.90) 
```

We make a term document matrix


```r
mTDM <- as.matrix(CorpusObj.tdm)
v <- sort(rowSums(mTDM),decreasing=TRUE)
d <- data.frame(word = names(v),freq=v)
head(d, 10)
```

```
##          word freq
## marvel marvel   32
## can       can   28
## found   found   28
## sign     sign   25
## one       one   25
## end       end   24
## get       get   24
## time     time   23
## infin   infin   21
## film     film   21
```

## Word Cloud

Finally we create the word cloud from the corpus object that we created in the last part.


```r
pal <- brewer.pal(9, "BuGn")
pal <- pal[-(1:2)]
png(paste0(getwd(),"/resources/wordcloud_sentiment/wordcloud.png"), width=1280,height=900)
wordcloud(d$word,d$freq, min.freq=300, scale=c(7,0.5),
          colors=brewer.pal(8, "Dark2"),  random.color= TRUE, random.order = FALSE)
dev.off()
```

```
## png 
##   2
```

Please note to see the word cloud check the png file. It is not the best practice to plot word cloud from a huge corpus on R console because of the limited resolution
