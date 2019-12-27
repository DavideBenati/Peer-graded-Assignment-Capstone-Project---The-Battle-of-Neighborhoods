# Peer-graded-Assignment-Capstone-Project---The-Battle-of-Neighborhoods
Peer-graded Assignment: Capstone Project - The Battle of Neighborhoods

# Week 2 Assignement

In this week, you will continue working on your capstone project.
---

# INTRODUCTION
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

# DATA

## In this section there will be a summary of the data that will be used for the completion of the project.

The principal source of data are the official statistics provided by Basel-Land website:
https://www.statistik.bs.ch/zahlen/tabellen/1-bevoelkerung/bestand-struktur.html
From this website will be possible to extract and scrumble:

- Name and area of the various districts:
![GitHub Logo](C:\ibm\Images\Quarters.jpg?raw=true "Basel Districts")
- Population data (Local and immigrants):

- Social Welfare quota

- Net worth distribution

- Pizzerias in the area 

It has be decided to use GeoPy: https://geopy.readthedocs.io/ for the Latitude and Longitude extrapolation and correlation with the various neighbourhoods.

We will also scramble data from Tripadvisor, in order to understand actual Pizzerias distribution and average ranking and price evaluation.
padvisor.com/Restaurants-g188049-Basel.html

These data will provide the answer to the following question:

There is a room to open a new Pizzeria in Basel and, if so, where to open it?

# METHODOLOGY

## In this section we discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed, if any, and what machine learnings were used and why.

