*The above files are written to produce:*

- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the current/most recent postcode of a user.
- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the postcode a user was in at the time when that user made a pageview.

*Design of the warehouse:*
![alt text](https://github.com/sashadeezauch/page_view/blob/main/Diagram.png?raw=true)

*Airflow DAG to automate the script:*
pageview_postcode.py
