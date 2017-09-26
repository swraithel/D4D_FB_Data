# Summarise_FB_Comments
Seth_Raithel  
`2017-09-26  




### Create Basic Agg Stats

Count:

- Number of comments per congressperson
- Number of unique users per congressperson
- Number of unique posts per congressperson


```r
load("C:/Users/Seth_Raithel/Desktop/fbtextmine/commentsfull.RData")

total_comments <-
  comments %>% count(name, sort = TRUE) %>% rename("total_no_of_comments" = n)
  
total_unique_users <-
  comments %>% distinct(name, user_id , keep_all = TRUE) %>%
  count(name, sort = TRUE) %>% rename("unique_engagers" = n)
  
total_posts <-
  comments %>% distinct(name, post_id, .keep_all = TRUE) %>%
  count(name) %>% rename("unique_posts" = n)
  
summary_congress <-
  left_join(total_comments, total_unique_users, by = "name")
  
summary_congress <-
  left_join(summary_congress, total_posts, by = "name")
```


### Export Basic Summary


```r
readr::write_csv(summary_congress,"Cali_FB_Comment_Stats.csv")
```


