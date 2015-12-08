
# Predicting Congressional Bill Outcomes #

Over the course of this quarter, we built a predictor that identifies which US bills will pass in the House and in the Senate. Our motivation for this project is to learn more about what strategic tools have the greatest marginal impact in Congress, and our starting hypothesis was that lobbying dollars spent in one direction would be the single most impactful factor.

The predictor is modeled on Congressional data from 1997 - 2010 from a wide range of sources. (We will go into further detail in the "Infrastructure" section.) We evaluated our system based on whether or not we were able to predict the outcome of a particular bill correctly.

<a name='infrastructure'></a>

## Data Sources & Infrastructure ##

We relied on several datasets to train our classifier. Specifically, we used:

#### U.S. Library of Congress' Bills Data ####

We retrieved bill data covering 1973-present as a bulk download from [thomas.gov](http://thomas.gov), an official source for legislative information that is run by the U.S. Library of Congress. Each document contains JSON for a particular bill, including identifying information, the outcome/status of the bill, amendment history, sponsor and co-sponsor information, details about the relevant congressional committees, and much more.

You can learn more about this dataset from the [@unitedstates project](https://theunitedstates.io/)'s wiki, found at [github.com/unitedstates/congress/wiki/Bills](http://github.com/unitedstates/congress/wiki/Bills).

#### MapLight's Congressional Bills Data ####

<img src='images/maplight-sample.png' style='float: right; width: 60%; margin: 20px'>

We relied most heavily upon [MapLight's meticulously curated data](http://maplight.org/us-congress/bill/search/description?page=0&solrsort=ds_last_action%20asc&namespace=map_bill_search) about the contributions given to members of Congress from interest groups that support or oppose various bills. You can find a screenshot of a bill profile page to the right.

We want to give a shoutout to the MapLight team's [fantastic work](http://maplight.org/content/about-maplight#howwedoit). Without their careful, nonpartisan analysis, this project would not have been possible.

The data was not available in a clean, structured format, so much of our effort was spent on extracting and preprocessing the information from MapLight's thousands of paginated webpages that contain the information we needed.

> TODO: What steps did we take to extract the data? Where can people find the scripts we used to do this?

We have made the structured data available [here]() so that others can play around with it too.

> TODO: add link on "here" to point to a zip file containing the bill data we used.

- For bills from previous congresses (i.e. >2 years old), if the status is “Referred to committee” or “Introduced” or “Reported to committee” then it’s a failure.
And we aren’t training on current congressional data anyways
- Possible Statuses:
    + **Enacted Laws:** Enacted bills and joint resolutions (both bills and joint resolutions can be enacted as law)
    + **Passed Resolutions:** Passed resolutions (for joint and concurrent resolutions, this means passed both chambers)
    + **Got A Vote:** Bills and joint/concurrent resolutions that had a significant vote in one chamber
    + **Failed Legislation:** Bills and resolutions that failed a vote on passage or failed a significant vote such as cloture, passage under suspension, or resolving differences
    + **Vetoed Bills (w/o Override):** Bills that were vetoed and the veto was not overridden by Congress
    + **Other Legislation:** Bills and resolutions that were introduced, referred to committee, or reported by committee but had no further action


```
<<[data/bill-outcome-statistics--1974-2015.csv]
```

#### GovTrack's Data

---

<!-- - [**U.S. Senate Lobbying Records:**](https://app.enigma.io/search/source/us.gov.senate.publicrecords.lobbying) Enigma offers lobbying information originally published by the Senate's public records department. Each row of this dataset corresponds to a lobbying transaction. Each transaction includes information about the lobbying client, the firm through which it is working, the industry to which the client belongs, the magnitude of the transaction in dollars, and several other pieces of metadata. We were disappointed to discover that the data did not include information on the recipients of lobbying funds nor the => left us with the challenge of
-->

Required joining the three datasets


<a name='data-exploration'></a>

## Data Exploration ##

k-means clustering


<a name='approach'></a>

## Approach ##

> Identify the challenges of building the system and the phenomena in the data that you're trying to capture. How should you model the task (e.g., using search, machine learning, logic, etc.)? There will be many ways to do this, but you should pick one or two and explain how the methods address the challenges as well as any pros and cons. What algorithms are appropriate for handling the models that you came up with, and what are the tradeoffs between accuracy and efficiency? Are there any implementation choices specific to your problem?
>
> Besides your primary approach(es), you should have two types of other ones, baselines and oracles. These are really important as they tell you how significant the problem you're solving is. Baselines are simple algorithms, which might include predicting the majority label, using a small set of hand-crafted rules, training a simple classifier, etc. Baselines are meant to be extremely simple, but you might be surprised at how effective they are. Oracles are algorithms that "cheat" and look at the correct answer or involve humans. If your problem has two components (identifying entities and classifying them), an oracle uses the correct answer for one of the components, and sees how well the other can do. Baselines give lower bounds and oracles give upper bounds on your performance. If this gap is too small, then you probably don't have an interesting enough task.

Features:

- absolute amount of money spent supporting and opposing the bill
- ratio of support:oppose
- which member of congress sponsored the bill
- number of amendments
- general issue topic (pre-categorized by the Library of Congress data)
- ...

Algorithms we tried:

- Naive Bayes
- SVM
- ...

#### Baseline ####

#### Oracle ####

#### Main Approach ####


<a name='literature-review'></a>

## Literature review ##

> Have there been other attempts to build such a system? Compare and contrast your approach with existing work, citing the relevant papers. The comparison should be more than just high-level descriptions. You should try to fit your work and other work into the same framework. Are the two approaches complementary, orthogonal, or contradictory?


<a name='error-analysis'></a>

## Error analysis ##

> Design a few experiments to show the properties (both pros and cons) of your system. For example, if your system is supposed to deal with graphs with lots of cycles, then construct both examples with lots of cycles and ones without to test your hypothesis. Each experiment should ask a concise question, such as: Do we need to model the interactions between the ghosts in Pac-Man? or How well does the system scale up to large datasets? Analyze the data and show either graphs or tables to illustrate your point. What's the take-away message? Were there any surprises?
