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

##Please find below some data sample:

{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import os\n",
    "import csv      # Import the csv module\n",
    "import pandas as pd\n",
    "import sys\n",
    "import numpy as np\n",
    "Basel_District = pd.read_csv('BaselDistricts.csv',header=0,encoding = 'unicode_escape')\n",
    "IncomeperDistrict = pd.read_csv('IncomeperDistrict.csv',header=0,encoding = 'unicode_escape')\n",
    "PopulationPerDistrict = pd.read_csv('PopulationPerDistrict.csv',header=0,encoding = 'unicode_escape')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Quartier</th>\n",
       "      <th>Hektar</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Altstadt Grossbasel</td>\n",
       "      <td>37,63</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Vorstdte</td>\n",
       "      <td>89,66</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Am Ring</td>\n",
       "      <td>90,98</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Breite</td>\n",
       "      <td>68,39</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>St. Alban</td>\n",
       "      <td>294,46</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Quartier  Hektar\n",
       "0  Altstadt Grossbasel   37,63\n",
       "1            Vorstdte   89,66\n",
       "2              Am Ring   90,98\n",
       "3               Breite   68,39\n",
       "4            St. Alban  294,46"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Basel_District.head()\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[0     Altstadt Grossbasel\n",
      "1               Vorstdte\n",
      "2                 Am Ring\n",
      "3                  Breite\n",
      "4               St. Alban\n",
      "5            Gundeldingen\n",
      "6              Bruderholz\n",
      "7              Bachletten\n",
      "8                Gotthelf\n",
      "9                  Iselin\n",
      "10             St. Johann\n",
      "11    Altstadt Kleinbasel\n",
      "12                  Clara\n",
      "13              Wettstein\n",
      "14            Hirzbrunnen\n",
      "15               Rosental\n",
      "16               Matthus\n",
      "17                Klybeck\n",
      "18          Kleinhningen\n",
      "19                 Riehen\n",
      "20              Bettingen\n",
      "Name: Quartier, dtype: object]\n"
     ]
    }
   ],
   "source": [
    "Quartier=[Basel_District[ 'Quartier']]\n",
    "print(Quartier)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Collecting geopy\n",
      "\u001b[?25l  Downloading https://files.pythonhosted.org/packages/80/93/d384479da0ead712bdaf697a8399c13a9a89bd856ada5a27d462fb45e47b/geopy-1.20.0-py2.py3-none-any.whl (100kB)\n",
      "\u001b[K     |████████████████████████████████| 102kB 4.7MB/s ta 0:00:01\n",
      "\u001b[?25hCollecting geographiclib<2,>=1.49 (from geopy)\n",
      "  Downloading https://files.pythonhosted.org/packages/8b/62/26ec95a98ba64299163199e95ad1b0e34ad3f4e176e221c40245f211e425/geographiclib-1.50-py3-none-any.whl\n",
      "Installing collected packages: geographiclib, geopy\n",
      "Successfully installed geographiclib-1.50 geopy-1.20.0\n",
      "Note: you may need to restart the kernel to use updated packages.\n"
     ]
    }
   ],
   "source": [
    "pip install geopy"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Am Ring, Basel, Basel-Stadt, 4003, Schweiz/Suisse/Svizzera/Svizra\n",
      "(47.5587744, 7.5774773)\n"
     ]
    }
   ],
   "source": [
    "from geopy.geocoders import Nominatim\n",
    "geolocator = Nominatim(user_agent=\"specify_your_app_name_here\")\n",
    "location = geolocator.geocode('Basel, Am Ring')\n",
    "print(location.address)\n",
    "print((location.latitude, location.longitude))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.DataFrame({'name': ['Basel, Altstadt Grossbasel','Basel, Vorstädte','Basel, Am Ring','Basel, Breite','Basel, St. Alban','Basel, Gundeldingen','Basel, Bruderholz','Basel, Bachletten','Basel, Gotthelf','Basel, Iselin','Basel, St. Johann','Basel, Altstadt Kleinbasel','Basel, Clara','Basel, Wettstein','Basel, Hirzbrunnen','Basel, Rosental','Basel, ','Basel Matthäus','Basel, Klybeck','Basel, Kleinhüningen','Basel, Riehen','Basel, Bettingen']})\n",
    "\n",
    "from geopy.geocoders import Nominatim\n",
    "geolocator = Nominatim(user_agent=\"specify_your_app_name_here\")\n",
    "\n",
    "from geopy.extra.rate_limiter import RateLimiter\n",
    "geocode = RateLimiter(geolocator.geocode, min_delay_seconds=1)\n",
    "df['location'] = df['name'].apply(geocode)\n",
    "\n",
    "df['Latitude and Longitude'] = df['location'].apply(lambda loc: tuple(loc.point) if loc else None)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>name</th>\n",
       "      <th>location</th>\n",
       "      <th>Latitude and Longitude</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Basel, Altstadt Grossbasel</td>\n",
       "      <td>(Altstadt Grossbasel, Basel, Basel-Stadt, 4001...</td>\n",
       "      <td>(47.5564274, 7.5882594, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Basel, Vorstädte</td>\n",
       "      <td>(Vorstädte, Basel, Basel-Stadt, Schweiz/Suisse...</td>\n",
       "      <td>(47.5526462, 7.5888037, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Basel, Am Ring</td>\n",
       "      <td>(Am Ring, Basel, Basel-Stadt, 4003, Schweiz/Su...</td>\n",
       "      <td>(47.5587744, 7.5774773, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Basel, Breite</td>\n",
       "      <td>(Breite, Basel, Basel-Stadt, Schweiz/Suisse/Sv...</td>\n",
       "      <td>(47.5518091, 7.6178526, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Basel, St. Alban</td>\n",
       "      <td>(St. Alban, Basel, Basel-Stadt, 4052, Schweiz/...</td>\n",
       "      <td>(47.5495654, 7.6050522, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Basel, Gundeldingen</td>\n",
       "      <td>(Gundeldingen, Basel, Basel-Stadt, Schweiz/Sui...</td>\n",
       "      <td>(47.5432192, 7.5914854, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>Basel, Bruderholz</td>\n",
       "      <td>(Bruderholz, Basel, Basel-Stadt, 4059, Schweiz...</td>\n",
       "      <td>(47.5307985, 7.5916242, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>Basel, Bachletten</td>\n",
       "      <td>(Bachletten, Basel, Basel-Stadt, 4054, Schweiz...</td>\n",
       "      <td>(47.5485663, 7.571726, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>Basel, Gotthelf</td>\n",
       "      <td>(Gotthelf, Basel, Basel-Stadt, Schweiz/Suisse/...</td>\n",
       "      <td>(47.5558192, 7.5709523, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>Basel, Iselin</td>\n",
       "      <td>(Iselin, Basel, Basel-Stadt, 4055, Schweiz/Sui...</td>\n",
       "      <td>(47.5621963, 7.5659985, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>10</th>\n",
       "      <td>Basel, St. Johann</td>\n",
       "      <td>(St. Johann, Basel, Basel-Stadt, Schweiz/Suiss...</td>\n",
       "      <td>(47.5690856, 7.5759341, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>11</th>\n",
       "      <td>Basel, Altstadt Kleinbasel</td>\n",
       "      <td>(Altstadt Kleinbasel, Basel, Basel-Stadt, Schw...</td>\n",
       "      <td>(47.5606996, 7.5933825, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>12</th>\n",
       "      <td>Basel, Clara</td>\n",
       "      <td>(Clara, Basel, Basel-Stadt, Schweiz/Suisse/Svi...</td>\n",
       "      <td>(47.5640853, 7.5966293, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>13</th>\n",
       "      <td>Basel, Wettstein</td>\n",
       "      <td>(Wettstein, Basel, Basel-Stadt, Schweiz/Suisse...</td>\n",
       "      <td>(47.560508, 7.6047949, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>14</th>\n",
       "      <td>Basel, Hirzbrunnen</td>\n",
       "      <td>(Hirzbrunnen, Basel, Basel-Stadt, 5068, Schwei...</td>\n",
       "      <td>(47.5688726, 7.6154703, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>15</th>\n",
       "      <td>Basel, Rosental</td>\n",
       "      <td>(Rosental, Basel, Basel-Stadt, Schweiz/Suisse/...</td>\n",
       "      <td>(47.5677078, 7.6014909, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>16</th>\n",
       "      <td>Basel,</td>\n",
       "      <td>(Basel, Basel-Stadt, Switzerland, (47.5581077,...</td>\n",
       "      <td>(47.5581077, 7.5878261, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>17</th>\n",
       "      <td>Basel Matthäus</td>\n",
       "      <td>(Matthäus, Basel, Basel-Stadt, Schweiz/Suisse/...</td>\n",
       "      <td>(47.5674388, 7.5915404, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>18</th>\n",
       "      <td>Basel, Klybeck</td>\n",
       "      <td>(Klybeck, Basel, Basel-Stadt, 4057, Schweiz/Su...</td>\n",
       "      <td>(47.5767978, 7.5901493, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>19</th>\n",
       "      <td>Basel, Kleinhüningen</td>\n",
       "      <td>(Kleinhüningen, Basel, Basel-Stadt, 4019, Schw...</td>\n",
       "      <td>(47.583376, 7.5975738, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>20</th>\n",
       "      <td>Basel, Riehen</td>\n",
       "      <td>(Riehen, Basel-Stadt, 4125, Schweiz/Suisse/Svi...</td>\n",
       "      <td>(47.5816927, 7.6479737, 0.0)</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>21</th>\n",
       "      <td>Basel, Bettingen</td>\n",
       "      <td>(Bettingen, Basel-Stadt, 4126, Schweiz/Suisse/...</td>\n",
       "      <td>(47.5714149, 7.6639831, 0.0)</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          name  \\\n",
       "0   Basel, Altstadt Grossbasel   \n",
       "1             Basel, Vorstädte   \n",
       "2               Basel, Am Ring   \n",
       "3                Basel, Breite   \n",
       "4             Basel, St. Alban   \n",
       "5          Basel, Gundeldingen   \n",
       "6            Basel, Bruderholz   \n",
       "7            Basel, Bachletten   \n",
       "8              Basel, Gotthelf   \n",
       "9                Basel, Iselin   \n",
       "10           Basel, St. Johann   \n",
       "11  Basel, Altstadt Kleinbasel   \n",
       "12                Basel, Clara   \n",
       "13            Basel, Wettstein   \n",
       "14          Basel, Hirzbrunnen   \n",
       "15             Basel, Rosental   \n",
       "16                     Basel,    \n",
       "17              Basel Matthäus   \n",
       "18              Basel, Klybeck   \n",
       "19        Basel, Kleinhüningen   \n",
       "20               Basel, Riehen   \n",
       "21            Basel, Bettingen   \n",
       "\n",
       "                                             location  \\\n",
       "0   (Altstadt Grossbasel, Basel, Basel-Stadt, 4001...   \n",
       "1   (Vorstädte, Basel, Basel-Stadt, Schweiz/Suisse...   \n",
       "2   (Am Ring, Basel, Basel-Stadt, 4003, Schweiz/Su...   \n",
       "3   (Breite, Basel, Basel-Stadt, Schweiz/Suisse/Sv...   \n",
       "4   (St. Alban, Basel, Basel-Stadt, 4052, Schweiz/...   \n",
       "5   (Gundeldingen, Basel, Basel-Stadt, Schweiz/Sui...   \n",
       "6   (Bruderholz, Basel, Basel-Stadt, 4059, Schweiz...   \n",
       "7   (Bachletten, Basel, Basel-Stadt, 4054, Schweiz...   \n",
       "8   (Gotthelf, Basel, Basel-Stadt, Schweiz/Suisse/...   \n",
       "9   (Iselin, Basel, Basel-Stadt, 4055, Schweiz/Sui...   \n",
       "10  (St. Johann, Basel, Basel-Stadt, Schweiz/Suiss...   \n",
       "11  (Altstadt Kleinbasel, Basel, Basel-Stadt, Schw...   \n",
       "12  (Clara, Basel, Basel-Stadt, Schweiz/Suisse/Svi...   \n",
       "13  (Wettstein, Basel, Basel-Stadt, Schweiz/Suisse...   \n",
       "14  (Hirzbrunnen, Basel, Basel-Stadt, 5068, Schwei...   \n",
       "15  (Rosental, Basel, Basel-Stadt, Schweiz/Suisse/...   \n",
       "16  (Basel, Basel-Stadt, Switzerland, (47.5581077,...   \n",
       "17  (Matthäus, Basel, Basel-Stadt, Schweiz/Suisse/...   \n",
       "18  (Klybeck, Basel, Basel-Stadt, 4057, Schweiz/Su...   \n",
       "19  (Kleinhüningen, Basel, Basel-Stadt, 4019, Schw...   \n",
       "20  (Riehen, Basel-Stadt, 4125, Schweiz/Suisse/Svi...   \n",
       "21  (Bettingen, Basel-Stadt, 4126, Schweiz/Suisse/...   \n",
       "\n",
       "          Latitude and Longitude  \n",
       "0   (47.5564274, 7.5882594, 0.0)  \n",
       "1   (47.5526462, 7.5888037, 0.0)  \n",
       "2   (47.5587744, 7.5774773, 0.0)  \n",
       "3   (47.5518091, 7.6178526, 0.0)  \n",
       "4   (47.5495654, 7.6050522, 0.0)  \n",
       "5   (47.5432192, 7.5914854, 0.0)  \n",
       "6   (47.5307985, 7.5916242, 0.0)  \n",
       "7    (47.5485663, 7.571726, 0.0)  \n",
       "8   (47.5558192, 7.5709523, 0.0)  \n",
       "9   (47.5621963, 7.5659985, 0.0)  \n",
       "10  (47.5690856, 7.5759341, 0.0)  \n",
       "11  (47.5606996, 7.5933825, 0.0)  \n",
       "12  (47.5640853, 7.5966293, 0.0)  \n",
       "13   (47.560508, 7.6047949, 0.0)  \n",
       "14  (47.5688726, 7.6154703, 0.0)  \n",
       "15  (47.5677078, 7.6014909, 0.0)  \n",
       "16  (47.5581077, 7.5878261, 0.0)  \n",
       "17  (47.5674388, 7.5915404, 0.0)  \n",
       "18  (47.5767978, 7.5901493, 0.0)  \n",
       "19   (47.583376, 7.5975738, 0.0)  \n",
       "20  (47.5816927, 7.6479737, 0.0)  \n",
       "21  (47.5714149, 7.6639831, 0.0)  "
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>District</th>\n",
       "      <th>Schweizer</th>\n",
       "      <th>Ausländer</th>\n",
       "      <th>Total</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Stadt Basel</td>\n",
       "      <td>110,524</td>\n",
       "      <td>67,368</td>\n",
       "      <td>177,892</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Altstadt Grossbasel</td>\n",
       "      <td>1,836</td>\n",
       "      <td>715</td>\n",
       "      <td>2,551</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Vorstädte</td>\n",
       "      <td>3,117</td>\n",
       "      <td>1,969</td>\n",
       "      <td>5,086</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Am Ring</td>\n",
       "      <td>6,978</td>\n",
       "      <td>4,160</td>\n",
       "      <td>11,138</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Breite</td>\n",
       "      <td>5,917</td>\n",
       "      <td>3,100</td>\n",
       "      <td>9,017</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              District Schweizer Ausländer    Total\n",
       "0          Stadt Basel   110,524    67,368  177,892\n",
       "1  Altstadt Grossbasel     1,836       715    2,551\n",
       "2            Vorstädte     3,117     1,969    5,086\n",
       "3              Am Ring     6,978     4,160   11,138\n",
       "4               Breite     5,917     3,100    9,017"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "PopulationPerDistrict.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>District</th>\n",
       "      <th>Mittelwert\\nin Fr.</th>\n",
       "      <th>Median\\nin Fr.</th>\n",
       "      <th>Gini-Koeffizient4</th>\n",
       "      <th>Mittelwert\\nin Fr. .1</th>\n",
       "      <th>Median\\nin Fr. .1</th>\n",
       "      <th>Summe\\nin Fr.</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Stadt Basel</td>\n",
       "      <td>66,842</td>\n",
       "      <td>48,126</td>\n",
       "      <td>0.515</td>\n",
       "      <td>9,503</td>\n",
       "      <td>5,140</td>\n",
       "      <td>980,878,199</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Altstadt Grossbasel</td>\n",
       "      <td>99,020</td>\n",
       "      <td>51,264</td>\n",
       "      <td>0.643</td>\n",
       "      <td>16,990</td>\n",
       "      <td>6,386</td>\n",
       "      <td>28,475,486</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Vorstädte</td>\n",
       "      <td>103,696</td>\n",
       "      <td>58,786</td>\n",
       "      <td>0.588</td>\n",
       "      <td>17,096</td>\n",
       "      <td>7,665</td>\n",
       "      <td>51,698,929</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Am Ring</td>\n",
       "      <td>77,051</td>\n",
       "      <td>54,114</td>\n",
       "      <td>0.518</td>\n",
       "      <td>11,446</td>\n",
       "      <td>6,497</td>\n",
       "      <td>70,710,469</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Breite</td>\n",
       "      <td>56,742</td>\n",
       "      <td>47,243</td>\n",
       "      <td>0.426</td>\n",
       "      <td>7,394</td>\n",
       "      <td>5,051</td>\n",
       "      <td>41,544,946</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              District Mittelwert\\nin Fr.  Median\\nin Fr.   Gini-Koeffizient4  \\\n",
       "0          Stadt Basel              66,842          48,126              0.515   \n",
       "1  Altstadt Grossbasel              99,020          51,264              0.643   \n",
       "2            Vorstädte             103,696          58,786              0.588   \n",
       "3              Am Ring              77,051          54,114              0.518   \n",
       "4               Breite              56,742          47,243              0.426   \n",
       "\n",
       "  Mittelwert\\nin Fr. .1 Median\\nin Fr. .1 Summe\\nin Fr.   \n",
       "0                 9,503             5,140    980,878,199  \n",
       "1                16,990             6,386     28,475,486  \n",
       "2                17,096             7,665     51,698,929  \n",
       "3                11,446             6,497     70,710,469  \n",
       "4                 7,394             5,051     41,544,946  "
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "IncomeperDistrict.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Flatiron Building, 175, 5th Avenue, Flatiron District, Manhattan Community Board 5, Manhattan, New York County, New York, 10010, United States of America\n",
      "(40.7410861, -73.9896298241625)\n"
     ]
    }
   ],
   "source": [
    "from geopy.geocoders import Nominatim\n",
    "geolocator = Nominatim(user_agent=\"specify_your_app_name_here\")\n",
    "location = geolocator.geocode(\"175 5th Avenue NYC\")\n",
    "print(location.address)\n",
    "print((location.latitude, location.longitude))"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}

