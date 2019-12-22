# Peer-graded-Assignment-Capstone-Project---The-Battle-of-Neighborhoods
Peer-graded Assignment: Capstone Project - The Battle of Neighborhoods

# Week 1 Assignement

Clearly define a problem or an idea of your choice, where you would need to leverage the Foursquare location data to solve or execute. Remember that data science problems always target an audience and are meant to help a group of stakeholders solve a problem, so make sure that you explicitly describe your audience and why they would care about your problem.

---

Describe the data that you will be using to solve the problem or execute your idea. Remember that you will need to use the Foursquare location data to solve the problem or execute your idea. You can absolutely use other datasets in combination with the Foursquare location data. So make sure that you provide adequate explanation and discussion, with examples, of the data that you will be using, even if it is only Foursquare location data.

# SECTION 1
## Scenario

As italian abroad, a potential customer would like to open a traditional italian pizzeria in Switzerland, more specifically in Basel.
This is a project that many people already attempted in the past, but only few succeeded.
Customer is really willing to start his new business, but he is afraid that a simple business plan would not be enough in order to succeed.
Some of the concern of the customers are:

1. How many restaurants are already in Basel
2. How many of them already offer ethnical food
3. How many Pizzeria are there in Basel and sorrounding
4. What is the best area where to open eventually
5. What could bethe expected income of his Pizzeria

There are also many other questions that customer could have not considered so far, but that an efficient data scientist could propose and include in his analyis. Some examples could be:

1. Criminality in various neighbouroud.
2. Corruption.
3. Average salaries for staff.
...

## Project

The idea of the project is the creation of a model capable to predict the success of a new Restaurant in a city similar to Basel (midsize european city).

A high level approach could be:

- Customer decides what kind of restaurnat wants to open and what is the target city
- A website like Tripadvisor scrapped for the restaurant list in the selected city
- Each restaurant is enriched with grographical data
- The historical crime within a predetermined distance of all venues are obtained
- A map is presented showing restaurant and crime statistics of the area
- Areas are also evaluated in term of prestige and number of inhabitants

The main data science aspect of this project including:

- Data Acquisition and Data Cleansing
- Data Analysis
- Machine Learning and Prediction

# SECTION 2

##In this section there will be a summary of the data that will be used for the completion of the project.

The principal source of data are the official statistics provided by Basel-Land website:
https://www.statistik.bs.ch/zahlen/tabellen/1-bevoelkerung/bestand-struktur.html
From this website will be possible to extract and scrumble:

- Name of the various districts
- Population data (Local and immigrants)
- Social Welfare quota
- Net worth distribution
- Criminality statistics
- Commericial activities

It has be decided to use GeoPy: https://geopy.readthedocs.io/ for the Latitude and Longitude extrapolation and correlation with the various neighbourhoods.

name	location	Latitude and Longitude
0	Basel, Altstadt Grossbasel	(Altstadt Grossbasel, Basel, Basel-Stadt, 4001...	(47.5564274, 7.5882594, 0.0)
1	Basel, Vorstädte	(Vorstädte, Basel, Basel-Stadt, Schweiz/Suisse...	(47.5526462, 7.5888037, 0.0)
2	Basel, Am Ring	(Am Ring, Basel, Basel-Stadt, 4003, Schweiz/Su...	(47.5587744, 7.5774773, 0.0)
3	Basel, Breite	(Breite, Basel, Basel-Stadt, Schweiz/Suisse/Sv...	(47.5518091, 7.6178526, 0.0)
4	Basel, St. Alban	(St. Alban, Basel, Basel-Stadt, 4052, Schweiz/...	(47.5495654, 7.6050522, 0.0)
5	Basel, Gundeldingen	(Gundeldingen, Basel, Basel-Stadt, Schweiz/Sui...	(47.5432192, 7.5914854, 0.0)
6	Basel, Bruderholz	(Bruderholz, Basel, Basel-Stadt, 4059, Schweiz...	(47.5307985, 7.5916242, 0.0)
7	Basel, Bachletten	(Bachletten, Basel, Basel-Stadt, 4054, Schweiz...	(47.5485663, 7.571726, 0.0)
8	Basel, Gotthelf	(Gotthelf, Basel, Basel-Stadt, Schweiz/Suisse/...	(47.5558192, 7.5709523, 0.0)
9	Basel, Iselin	(Iselin, Basel, Basel-Stadt, 4055, Schweiz/Sui...	(47.5621963, 7.5659985, 0.0)
10	Basel, St. Johann	(St. Johann, Basel, Basel-Stadt, Schweiz/Suiss...	(47.5690856, 7.5759341, 0.0)
11	Basel, Altstadt Kleinbasel	(Altstadt Kleinbasel, Basel, Basel-Stadt, Schw...	(47.5606996, 7.5933825, 0.0)
12	Basel, Clara	(Clara, Basel, Basel-Stadt, Schweiz/Suisse/Svi...	(47.5640853, 7.5966293, 0.0)
13	Basel, Wettstein	(Wettstein, Basel, Basel-Stadt, Schweiz/Suisse...	(47.560508, 7.6047949, 0.0)
14	Basel, Hirzbrunnen	(Hirzbrunnen, Basel, Basel-Stadt, 5068, Schwei...	(47.5688726, 7.6154703, 0.0)
15	Basel, Rosental	(Rosental, Basel, Basel-Stadt, Schweiz/Suisse/...	(47.5677078, 7.6014909, 0.0)
16	Basel,	(Basel, Basel-Stadt, Switzerland, (47.5581077,...	(47.5581077, 7.5878261, 0.0)
17	Basel Matthäus	(Matthäus, Basel, Basel-Stadt, Schweiz/Suisse/...	(47.5674388, 7.5915404, 0.0)
18	Basel, Klybeck	(Klybeck, Basel, Basel-Stadt, 4057, Schweiz/Su...	(47.5767978, 7.5901493, 0.0)
19	Basel, Kleinhüningen	(Kleinhüningen, Basel, Basel-Stadt, 4019, Schw...	(47.583376, 7.5975738, 0.0)
20	Basel, Riehen	(Riehen, Basel-Stadt, 4125, Schweiz/Suisse/Svi...	(47.5816927, 7.6479737, 0.0)
21	Basel, Bettingen	(Bettingen, Basel-Stadt, 4126, Schweiz/Suisse/...	(47.5714149, 7.6639831, 0.0

These data will provide the answer to the following questions:
What is the ranking of the three best neighbourhood where to open a pizzeria?


