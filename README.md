# ![Project Header Image](images/project_header_img.png)

# The Stress-Sighting Hypothesis
### A Data-Driven Analysis of Global Events and Reports of the Unknown.

**The Stress-Sighting Hypothesis** has the project goal of investigating whether there is a meaningful correlation between the frequency of reported UFO sightings and periods of heightened cultural, political or global stress, using historical event data and publicly reported sightings. 

---

## Dataset Content
* Our primary dataset is taken from the Kaggle dataset 'UFO Sightings' found here: https://www.kaggle.com/datasets/NUFORC/ufo-sightings/data

It is a cleaned public dataset derived from NUFORC (National UFO Reporting Center) reports. It contains 80,332 records of reported UFO sightings worldwide, spanning over a century.

### Dataset Overview: 
- **Date Range:** January 1st, 1910 - September 9, 2013
- **Number of Records:** 80,332
- **Primary Columns:**
    - **datetime:** Date and time of the sighting
    - **city, state, country**: Geographic location
    - **shape:** Reported shape of the object (e.g., disk, light, triangle)
    -**duration (seconds), duration (hours/min):** Estimated duration
    - **comments:** Eyewitness description
    - **latitude, longitude:** Coordinates

This dataset will be aggregated by year to explore temporal trends in UFO reporting and merged with the global_stress_events dataset to investigate possible correlations. 

- Our secondary dataset is the **global_stress_events.csv**
This dataset aims to contextualise major geopolitical, environmental, economic, and cultural events that are likely to contribute to collective public stress or uncertainty.

Rather than relying on a single predefined dataset, this list was manually curated to ensure it aligned specifically with the project’s thematic focus: the intersection of cultural perception, public anxiety, and the unknown. Events were selected based on their:
- Global or national scale of impact
- Media visibility and saturation
- Potential to influence public mood, fear, or psychological tension
- Relevance to war, political instability, health crises, economic collapse, or culturally significant media related to UFOs and extraterrestrial life

### Dataset Overview:
- **Date Range:** 1947-2023
- **Number of Records:** 35
- **Primary Columns:**
    - **year:** The year the event occurred
    - **event:** Name or description of event
    - **category:** Type of event (e.g., War, Cultural, Environmental)
    - **region:** Geographical scope (e.g., Global, USA, Europe)
    - **severity_(1-5):** Subjective rating of perceived societal impact
    - **notes:** Brief explanation of the event's significance

This dataset was designed as a companion to the UFO sightings data, to support hypothesis testing via statistical analysis and regression modelling. 
Whilst not exhaustive, this dataset serves as a representative proxy for fluctuations in global psychological stress and its potential relationship with the frequency of UFO reports. Future iterations could expand this dataset or refine severity scoring using sentiment analysis or survey data.

Severity ratings were assigned subjectively, based on the perceived scale and psychological weight of each event, and are intended to offer an optional variable for weighted analysis. 

## Business Requirements
In an era shaped by information saturation, political polarisation, and global crises, public perception is increasingly complex and emotionally charged. For journalists, researchers, and communicators, understanding how people respond to uncertainty is as important as the events themselves.

This project explores the potential relationship between **reported UFO sightings** and **global stress events**, not to investigate extraterrestrial phenomena, but to examine whether these sightings reflect **underlying patterns of public anxiety, media influence, and cultural tension.**

The outcome is a data-driven dashboard designed to support those working at the intersection of **data**, **storytelling**, and **public insight**.

### Persona & User Story:
![Alex Holloway – Persona Card](images/alex_holloway_persona_card.png)

**Alex Holloway** is an investigative journalist, known for in-depth features that combine cultural analysis with data storytelling. They work with both independent media outlets and major publishers, seeking to explore how society processes uncertainty — from political unrest to media myths.

### Alex's Requirements:
- **Reveal Patterns**

Alex needs to identify correlations between historical periods of stress and spikes in UFO reporting - fast, clearly and without technical issues. 

- **Narrative Context**

They want to explore not just *when* things happened, but *why it matters.* Explanatory text and annotations support deeper storytelling.

- **Usable Insights**

Our charts and summaries must be easy to extract for use in articles or reports, including explanatory captions and legends.

- **Trustworthy Structure**

The data pipeline must be transparent, ethical and well-documented to ensure and maintain credibility in their journalistic work.

### Value Proposition:
Our Dashboard must empower users like Alex to:
- Translate complex data into cultural insight
- Frame journalistic stories with empirical evidence
- Uncover social signals hiding in unconventional data
- Offer the audience a grounded perspective on how fear, media, and uncertainty intersect. 

## Hypotheses
This project explores whether there is a measurable relationship between periods of global stress and the volume of reported UFO sightings. The following hypotheses will be tested using aggregated time-series data and statistical methods, including linear regression.

### **H1: There is a positive correlation between the number of glabal stress events in a given year and the number of UFO sightings.**

**Validation Approach:**
- Aggregate UFO sightings by year
- Count stress events per year from the global stress events dataset
- Perform Pearson correlation and linear regression using stress_event_count as the independent variable
- Visualise results with a scatter plot and regression line

### **H2: Years with higher total stress severity scores are associated with a greater number of UFO sightings.**

**Validation Approach:**
- Sum severity scores per year (severity_sum)
- Regress *sightings_per_year* against *severity_sum*
- Compare R² and regression coefficients with **H1**
- Visualise and interpret strength of correlation

### **H3: Cultural media events, (such as the release of UFO-themed films or television series) correspond with noticeable short-term spikes in reported sightings.**

**Validation Approach:**

- Flag key media release years in the dataset (e.g., The X-Files in 1993, Independence Day in 1996)
- Visually inspect anomalies in *sightings_per_year* via time-series plots
- Compare spike magnitudes to adjacent years to investigate temporal influence 

---

## Project Plan
### Data Cleaning and Feature Engineering Summary

The UFO dataset underwent comprehensive cleaning to ensure analytical reliability. Key steps included:

- **Standardising column names** to lowercase with consistent formatting.
- **Handling missing values:**
  - Filled missing 'country', 'state', and 'shape' values with 'unknown'.
  - Removed 694 rows (~0.86%) where 'datetime' was missing or malformed, resulting in invalid 'year' values.
- **Cleaning problematic numeric columns:**
  - Converted 'duration (seconds)' and 'latitude' to numeric using 'pd.to_numeric()' with coercion.
  - Dropped 4 rows with invalid or non-numeric duration/latitude values.
- **Ensuring valid data ranges:**
  - Confirmed all latitude/longitude values were within Earth’s bounds.
  - Verified 'year' column ranged between 1947 and 2013 to align with the global stress dataset.
- **Dropped duplicate rows:** 2 exact duplicate entries were removed.
- **Converted data types:**
  - 'datetime' and 'date_posted' columns converted to proper datetime format.
  - Categorical fields ('country', 'state', 'shape') cast to 'category' type for efficient storage.
  - 'year' column cast to 'int' after NaNs were removed.

### Feature Engineering Summary

To prepare for analysis and regression, the following features were created:

- **'year'** extracted from the 'datetime' column to serve as a temporal anchor for all analysis.
- **'sightings_per_year'**: A new summary DataFrame was created by grouping the cleaned UFO dataset by 'year', counting the number of sightings annually.
- The global stress dataset was also cleaned:
  - Columns standardised and typed correctly.
  - Aggregated into a yearly summary with:
    - 'stress_event_count' (number of stress events per year)
    - 'severity_sum' (total of severity scores per year).
- Both datasets were filtered to a shared timeframe (1947–2013) and merged using a **left join**, preserving years with zero stress events for baseline comparison.
- Missing values in the merged dataset (due to non-stress years) were filled with '0' to maintain continuity in analysis.

## The rationale to map the business requirements to the Data Visualisations
* List your business requirements and a rationale to map them to the Data Visualisations

## Analysis techniques used
* List the data analysis methods used and explain limitations or alternative approaches.
* How did you structure the data analysis techniques. Justify your response.
* Did the data limit you, and did you use an alternative approach to meet these challenges?
* How did you use generative AI tools to help with ideation, design thinking and code optimisation?

## Ethical considerations
* Approximately 12% of the rows in our UFO dataset were missing a recorded country. While it is technically possible to infer country from latitude and longitude via reverse geocoding, this was not implemented at scale due to performance and ethical limitations around API usage.

Because this project is primarily concerned with **yearly patterns on a global scale**, the absence of country-level information does not significantly impact the core analysis or hypotheses being tested.

## Dashboard Design
* List all dashboard pages and their content, either blocks of information or widgets, like buttons, checkboxes, images, or any other item that your dashboard library supports.
* Later, during the project development, you may revisit your dashboard plan to update a given feature (for example, at the beginning of the project you were confident you would use a given plot to display an insight but subsequently you used another plot type).
* How were data insights communicated to technical and non-technical audiences?
* Explain how the dashboard was designed to communicate complex data insights to different audiences. 

## Unfixed Bugs
* Please mention unfixed bugs and why they were not fixed. This section should include shortcomings of the frameworks or technologies used. Although time can be a significant variable to consider, paucity of time and difficulty understanding implementation are not valid reasons to leave bugs unfixed.
* Did you recognise gaps in your knowledge, and how did you address them?
* If applicable, include evidence of feedback received (from peers or instructors) and how it improved your approach or understanding.

## Development Roadmap
* What challenges did you face, and what strategies were used to overcome these challenges?
* What new skills or tools do you plan to learn next based on your project experience? 

## Deployment

## Main Data Analysis Libraries
- Python
- Pandas
- NumPy
- Seaborne
- MatPlotLib
- Plotly
- SKLearn



## Credits 

* In this section, you need to reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism. 
* You can break the credits section up into Content and Media, depending on what you have included in your project. 

### Content 

- The text for the Home page was taken from Wikipedia Article A
- Instructions on how to implement form validation on the Sign-Up page was taken from [Specific YouTube Tutorial](https://www.youtube.com/)
- The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

- The photos used on the home and sign-up page are from This Open-Source site
- The images used for the gallery page were taken from this other open-source site



## Acknowledgements (optional)
* Thank the people who provided support through this project.
