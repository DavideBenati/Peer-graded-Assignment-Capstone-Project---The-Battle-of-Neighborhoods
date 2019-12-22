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


These data will provide the answer to the following question:

What is the ranking of the three best neighbourhood where to open a pizzeria?

##Please check Week1 file for data samples.
