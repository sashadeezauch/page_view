<h1>*The above files are written to produce:*<h1>

- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the current/most recent postcode of a user.
- Number of pageviews, on a given time period (hour, day, month, etc), per postcode - based on the postcode a user was in at the time when that user made a pageview.

<h1>*Design of the warehouse:*<h1>
![alt text](https://github.com/sashadeezauch/page_view/blob/main/Warehouse%20Diagram.png?raw=true)

<h1>*Airflow DAG to automate the script:*<h1>
pageview_postcode.py
