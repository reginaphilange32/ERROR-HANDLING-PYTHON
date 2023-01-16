# ERROR-HANDLING-PYTHON

# HOW TO SOLVE ERROR DURING IMPORTING DPLYR RVEST XML FOR R WEBSCRAPING

install.packages("dplyr")
install.packages("rvest")
library(xml2)
library(dplyr)
library(rvest)




url = "https://www.imdb.com/search/title/?title_type=feature&num_votes=25000,&genres=adventure&sort=user_rating,desc"
page =read_html(url)
movie_title = page %>% html_nodes(".lister-item-header a") %>% html_text()
View(movie_title)

movie_relyear = page %>% html_nodes(".text-muted.unbold") %>% html_text()
movie_relyear

imdbdf50 = data_frame(movie_title,movie_relyear)
View(imdbdf50)

#########################################
