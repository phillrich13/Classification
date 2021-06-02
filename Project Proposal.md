# Austin Animal Center Outcome Classification

## Question
### Framing
I am volunteering with the Austin Animal Center to develop a classification model to help them understand likely outcomes for newly acquired pets.

### Benefits
The Austin Animal Center wants to be able to predict likely outcomes with newly received animals so that they better plan a few things:
* Space for new animals, may need to transfer animals with outcomes associated with long term stays to make room for more urgent situations
* Budget considerations, long term animals require more money and if they can better understand the incoming animals they can better plan their budget and request more funding
* Pre-emptive care and potential change in process for animals predicted for Euthanasia

## Data
### Source
The Austin Animal Center has 2 hourly updated data sets. One is for [animal intakes](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Intakes/wter-evkm) and has descriptions for each animal encounter. There is also an [outcomes](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Outcomes/9t4d-g238) data set which details what happened with each animal encounter and gives a final outcome.

~120k records

### Individual Sample
One sample is 1 encounter with 1 animal. If an animal is received in say January, then adopted out. If the same animal is seen in June, then that is 2 separate records, instead of updating the first record.

### Features/Characteristics
* Location (city)
* Time of Day animal is received (likely broken out into 10 pm - 6 am for stealthy/emergency drop-offs, normal hours for standard drop-offs)
* How it was taken in (stray, public assistance, owner surrender, etc.)
* Intake Condition (sick, normal, etc.)
* Animal Type (Cat, Dog, Bird, Other)
* Sex on intake (male/female)
* Neuter/Spayed Status
* Age on intake (potentially use neo-natal, kitten/puppy, adult groupings)
* Breed (probably not, over 1000 breeds. May go 'Mix' vs. 'Not Mix')
* Color (may just go multi-color vs 1 color, as there are 599 listed color type/combos)

### Target
Animal Stay outcome:
* Adoption
* Transfer
* Return to Owner
* Euthanasia
* Death (non-Euthanasia)
* There are ~200 records with other outcomes, will have to determine how to address

## Tools
### Meeting Tools Requirements
I will use pandas, scikitlearn, and any other python packages for the modeling portions.

Visualization portion will be dependent on time availabe to me. Tableau is preferable.

## MVP
A Random Forests model to predict the outcome based on the listed features above.

