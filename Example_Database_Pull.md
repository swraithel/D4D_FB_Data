```python
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine('CONNECTION_INFO_HERE')

#page information is stored here
df_pages = pd.read_sql_query("SELECT * FROM page_facebook",con=engine)

#comments are stored here
df_comments = pd.read_sql_query("SELECT * FROM comment_facebook",con=engine)


#example of query
# Get the comments associated with California districts 13,15,17 (Bay Area ish)
df_pages_a = df_pages[(df_pages['district'].isin(['13','15','17'])) & (df_pages['state'] == 'California')]
df_comments_a = df_comments[df_comments['page_id'].isin(df_pages_a['page_id'].values)]
```
