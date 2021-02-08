*The above files are written to produce:*

- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the current/most recent postcode of a user.
- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the postcode a user was in at the time when that user made a pageview.

*Design of the warehouse:*
![alt text](https://github.com/sashadeezauch/page_view/blob/main/Diagram.png?raw=true)

*Tables:*

<h4>bi_db.users_extract:<h4> list of user ids and their current postcode. Updated once a day.
bi_db.pageviews_extract: list of pages visited, user ids and timestamp. Updated every hour but
only contains one hour worth of data.
bi_analytics.pageviews_user_history: used to record the list of all pageview extract along with their user’s
postcode at the time. Its needed because pageviews_extract is being truncated after each run and is only a
1hr snapshot of pageviews. The table is denormalised by adding users’ postcode, its needed to record the
postcode at the time of pageview.
bi_analytics.pageview_postcode_history_count : used to record the count of pageviews of
pageviews_user_history at a specific date (yyyy-mm-dd), hour, and postcode as of time visit (from
pageviews_user_history table) .

bi_analytics.pageview_postcode_now_count : used to record the count of pageviews of
pageviews_user_history at a specific date (yyyy-mm-dd), hour, and recent user’s postcode. Since
users_extract has the up-to-date user info, it is used to join with Pageviews_user_history to get the recent
postcode after truncating the historical data. But this heavy operation only need to be done once a day
because users_extract gets updated only once a day. Therefore, for hourly runs, Pageviews_user_history is
enough.

*Airflow DAG to automate the script:*
pageview_postcode.py -- to run everyday at 1am 
