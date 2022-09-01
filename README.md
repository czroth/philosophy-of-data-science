# Personal Philosophy of Data Science

## Introduction

This document describes the *What* and *Why* of Data Science, and does not specifically address the *How*.
It is meant to give insight into what I do, and why I do it.

This document is a work in progress. I hope discussions on these and other related topics expand and refine this document.

I'll start with a few definitions which I'll expand on the the [details](#details) section, and then look at the [responsiblities](#responsibilities) of the Data Scientist.

**Data**
is a set of observations (usually quantitative) collected to provide insight into a broad field of inquiry, or to answer a specific set of questions.

A **Data Scientist**
is someone capable of [reducing](#the-data-pipeline-data-reduction) data from the observations down to these insights or answers.
A Data Scientist uses a variety of analysis tools to derive these results.
The work of a Data Scientist also involves the overall management of data, from its collection through its distribution.
As the field of Data Science is still being pioneered, problem-solving is an essential skill for a Data Scientist.

## Details

### The nature of data

**Datasets**
Data is often part of a Dataset, which is a collection of variables with some common dimension or dimensions. Often one of the dimensions is temporal or spacial.

**Data Collection** 
is the process of gathering data. The process is usually via a digial recording device, but can also be through an analog recording device or human observation. Care must be taken to avoid introducing sampling bias into the data. Often the first [reduction](#data-reduction) performed is a calibration step to characterize for and remove biases.

#### Synthetic Data

**Synthetic Data** is data generated to stand in place of observed data.
Synthetic data is often generated during the planning stage before the creation of the data collection device, to help inform its design.
Synthetic data can be used to design the stages of [reduction](#the-data-pipeline-data-reduction) before real data is available. It can be used in the testing and validation stages of Continuous Integration.
The work of producing realistic synthetic data can help the Data Scientist better understand the nature of the data.   

#### Data Life-Cycle

The Life-Cycle of Data typically starts with [synthetic data](#synthetic-data) used to prepare and plan for actual observations.
While the observations are being collected, the dataset is continually growing and is in a dynamic state. Any data reductions that depend on the dataset as a whole will need to be re-run as more data is collected. 
Once the period of observation is over, the data is in a static (mature) state.
Eventually, the data will either be deleted, or [archived](#archiving) depending on the residual value of the data.

#### Public and Private Data

Data can be public or private. For more on the proper handling of private data, see [privacy](#privacy).

### The Data Pipeline (Data Reduction) 

The Data Pipeline is a set of Data Reduction step. The process starts with raw data and ends with the sought after results.
In the trivial case this invoves a single reduction step, such as finding the mean weight of a collection of objects.
More often this process involes a number of dependent reduction steps, each one transforming the data into another form.

Data Reduction can involve physical modelling, regression, optimization, machine learning, statistical methods, dimensional transformation, and more.
These processes are the *How* of Data Science and most often represent the core of what a Data Scientist does and where they spend their time.

Some pipeline steps may introduce additional data from an external dataset.

#### An Example Pipeline

Most of my Data Science career was spent on the [OSIRIS](https://research-groups.usask.ca/osiris/) satellite mission. Here is a simplified outline of the data pipeline.

| Stage | Method | Dimensions | Size |
| --- | --- | --- | --- |
| Radiance data of the atmosphere | Collection | Time, Pixel | ~10 TB |
| Calibration | Optimization & Regression | Time, Wavelength | ~10 TB |
| Ozone Profiles | Physical Modelling & Optimization | Time, Geolocation (lat/lon), Altitude, Ozone Density | ~10 GB |
| Ozone Climatology | Statistics & Dimensional Transform | Time, Binned latitude, Binned Altitude | ~10 MB |
| Decadal Trends | Regression | Binned latitude, Binned Altitude | ~100KB |

*The physical modelling step requires other atmospheric data from an outside dataset (NASA / MERRA2).*

Most of the above pipeline reductions involve additional sub-steps, but the overall picture illustrates the process and a typical reduction in size of the intermediate pipeline products. 

## Responsibilities
The simplist way for me to break down the *Why* of Data Science is to consider the responsibilities of the Data Scientist through the lens of *Who* I owe those responsibilities to.
I break this down into the following four categories:
* the [craft](#responsibilities-owed-to-the-craft) itself,
* my [employer](#responsibilities-owed-to-the-employer), 
* the [public](#responsibilities-owed-to-the-public), and
* my [guild](#responsibilities-owed-to-the-guild) (other Data Scientists). 

### Responsibilities Owed to the Craft

#### Maintenance

In the way a gardener feels a responsibility and affinity to the garden they tend, a Data Scientist has a similar affinity to their data.
The data and analysis tools should be well maintained and documented.
Common work-flows and practice with other Data Scientists make for fewer mistakes and more efficient work when collaborating.

### Responsibilities Owed to the Employer

#### Business Feedback

Usually, the primary task of the Data Scientist is to solve problems related to their service or product,
i.e., the goals flow downstream to the Data Scientist.
However, the Data Scientist should work with Strategic Management and provide feedback to inform business decision-making, considering such things as where the Data Science department's effort will be most profitable.

#### Relationship Between the Data Scientist and Other Departments

Like most departments in a business, Data Science interacts with a number of others in the pursuit of business goals.
The Data Scientist is more productive when they have a working knowledge of neighbouring departments, such as IT and IT Security, Engineering, Marketing, Web Development, etc.
An appreciation for neighbouring departments will help align the Data Scientist's work to the overall goals of their employer and also help the Data Scientist be more creative in problem solving.

### Responsibilities Owed to the Public

#### Archiving

At the end of the data's [life cycle](#data-life-cycle) an evaluation should take place to determine if the data should be archived for possible future analysis or data auditing.
Future analysis tools will likely yield greater and more accurate results that present tools.
If the results of a future, better analysis results could have practical or historical value (and the archival costs are not prohibitive) archiving the data should be considered.

If the result of the evaluation is that the data no longer has value relative to its storage cost, the space should be freed up.
Practically, this means scheduling data reviews to make and follow through on these determinations. Not holding to this discipline results in a larger data footprint than required.

#### Privacy

It is the responsibility of the Data Scientist (and IT Security) to prevent the leakage of private data.
No matter how it is collected, data that contains sensitive information or that is personal in nature needs to be protected.
The Data Scientist can not be passive in this matter. Nor is it enough to be reactive only; a proactive role must be taken to ensure the protection of private data and risk to the related risk to individuals, groups, or property.
For example:
* Where is the data collected?
* Where are the data and derivative products stored?
* Who is trusted to process the data?
* How is the data distributed and who is it distributed to?

When anonymizing data, be conscious of the potential to de-anonymizing data by combining information from several datasets.

Along the same lines, where data is sensitive in nature, the Data Scientist needs to ensure its collection involves the informed consent of the parties involved. 

#### Truth

A commitment to accurately represent data is an ethical imperative of the Data Scientist.
Statements like "Can you change the data to say this?" or "How much data do you have to remove so that the results are different?" should immediately raise red flags.
One of the foundational aspects of a customer / business relationship is trust. As the manipulation of data damages trust, it should be avoided on both business and ethical grounds.
Therefore, there is no conflict between business goals and the imperative to represent data accurately.

Sometimes, data is corrupt and needs to be evaluated to see if it can be corrected and/or removed, but this should not be used as an excuse to simply remove unwanted data.

#### Auditing

The requirement to the commitment to truth often consequentially leads to leaving a data audit trail that demonstrates how processing data led sequentially from A to B to C.
Practically this means using versioning tools like Git and along with documentation that describes what inputs and versioned tools produced which outputs.

### Responsibilities Owed to the Guild

#### Data Science Ecosystem

The field of Data Science consists largely in the maturing set of Data Scientists and their tools.
As each individual Data Scientist benefits from the contribution of others to the field, so each should consider how they can make their own contribution back to the ecosystem.
Some examples are:
* Mentoring a less experienced Data Scientist.
* Committing to an open-source Data Science package.
* Contributing to an open-source Data Science foundation.

#### Usability

When distributing datasets, the goal should be to make it easy for other Data Scientists to use. 
Consider the spectrum from poorly documented binary files to self-describing, cross-platform, data containers like HDF.
The former takes a day just to read and sets a high cost to data usage; whereas the latter can be opened in less than 15 minutes on almost any environment.
Remember, a year from today, the person most likely to have open and learn how to use your data is yourself.

## Final Thoughts

Other ideas for this material:
* With a few modifications, this document could be reworked for use as a Data Science homepage in a documentation system.
* There may be opportunity to use this material as the basis for a talk at a Data Science conference.
  * Most talks revolve around defining a problem and then describing its solution, i.e., the *How* of Data Science.
  * To compliment that, a talk on the *Why* of Data Science may be a welcome addition and spark conversation.
