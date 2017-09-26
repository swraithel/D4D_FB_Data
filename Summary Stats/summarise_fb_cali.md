# Summarise_FB_Comments
Seth_Raithel  
`r Sys.Date()`  




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

DT::datatable(summary_congress)
```

<!--html_preserve--><div id="htmlwidget-464c39d6b7f4409df9be" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-464c39d6b7f4409df9be">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82"],["Congressman Adam Schiff","Congresswoman Barbara Lee","Congressman Eric Swalwell","Congressman Mark Takano","Congresswoman Jackie Speier","Congressman Ami Bera","Congressmember Karen Bass","Congressman John Garamendi","Congressman Raul Ruiz, MD","La Jornada Baja California","Clima La Paz B. California Sur","Congresswoman Susan Davis","Congressman Brad Sherman","Congressman Jared Huffman","Congressman Scott Peters","Congresswoman Julia Brownley","California State University, Los Angeles","Congresswoman Anna Eshoo","Congresswoman Doris O. Matsui","Mike Levin","Congresswoman Norma Torres","Congressman Salud Carbajal","Congressman Jerry McNerney","Visit La Quinta - California","Ammar Campa for Congress","Congressman Juan Vargas","Congressman Jim Costa","Barbara Lee","Doris Matsui","Jimmy Panetta for Congress","Harley Rouda","Julia Brownley for Congress","Wendy Reed for Congress","Mercado La California","Salud Carbajal For U.S. Congress","Norma Torres for Congress","Robert Owen","Nanette Barragán for Congress","Stephen Jaffe For Congress","We Support Congresswoman Maxine Waters","Katie Hill for Congress","Phil Janowicz for Congress","Jackie Speier","Laura Oatman","Andrew Janz for Congress","Brad Sherman","Marty Walters for Congress","La California","Dave Min for Congress","Dennis Duncan For Congress","Roza Calderon for Congress 2018","Glenn Jensen for Congress","Dr. Hans Keirstead for Congress","Brian Forde for Congress","Dotty Nygard For Congress CD-10","Paul Kerr","Judy Chu for Congress","Tony Zarkades for Congress","Microbar La California","Anna Eshoo for Congress","Josh Butner for Congress","Gil Cisneros for Congress","Jessica Holcombe for Congress","Sam Jammal For Congress","Jim Costa for Congress","Wendy Reed Not for Congress","Grace Napolitano for Congress","Los callegones de Los Angeles California","US Congresswoman Maxine Waters","Michael Kotick for Congress","Jessica Heredia PLG Estates","Lucille Roybal-Allard","TJ Cox for Congress","Boyd Roberts For Congress","Katie Porter for Congress California CD-45","MyFit Apparel","Brad Westmoreland for Congress","Defeat Congresswoman Karen Bass in 2018","Lori Susan Kuhn","Ro khanna For Congress","Seth Vaughn for Congress","realist films"],[83213,62322,60865,60723,47338,37060,28325,28247,24667,19580,18169,16839,15704,15512,14766,12718,11130,9761,9464,5838,5110,4851,4837,4360,4087,3739,3654,3352,1771,1037,968,862,820,785,715,700,629,548,528,516,501,496,481,458,419,367,367,303,265,243,234,203,157,147,136,125,96,83,77,76,75,70,70,57,52,40,39,34,21,20,19,13,11,9,5,4,3,2,2,2,2,1],[31205,25085,15469,20913,17710,10148,15050,11287,9143,8037,6138,5251,8930,6139,4999,4616,5561,4169,4158,2334,1907,2067,2254,2378,3428,1782,2239,1686,968,587,634,520,212,641,435,294,429,370,296,186,268,233,252,365,220,269,104,265,180,112,132,54,117,136,110,104,66,21,69,53,49,53,59,46,36,11,34,31,12,18,16,12,11,7,2,2,2,2,2,2,1,1],[2304,2494,2835,1293,2647,2500,2245,2432,1324,4014,1430,1689,627,935,1445,1082,2129,685,1275,318,1179,199,916,1125,105,537,738,810,336,194,115,157,361,129,199,191,80,148,138,19,139,153,81,36,92,62,37,26,71,69,90,111,45,11,40,23,34,25,26,33,33,26,30,16,17,12,20,10,10,10,18,7,7,7,4,4,2,2,1,1,1,1]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>name<\/th>\n      <th>total_no_of_comments<\/th>\n      <th>unique_engagers<\/th>\n      <th>unique_posts<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[2,3,4]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


### Export Basic Summary


```r
readr::write_csv(summary_congress,"Cali_FB_Comment_Stats.csv")
```


