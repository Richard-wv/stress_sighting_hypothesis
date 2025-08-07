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

### **H1: There is a positive correlation between the number of global stress events in a given year and the number of UFO sightings.**

**Validation Approach:**

To test this hypothesis, we:

- Created a lagged version of the 'severity_sum' and 'stress_event_count' columns to account for delayed public or psychological response to global stress events.
- Calculated the correlation between the lagged severity and annual UFO sighting counts.
- Built a linear regression model using 'severity_sum_lag1' as the predictor for 'sightings_per_year'.
- Visualised the relationship using a regression plot.

### **Results & Conclusion:**

![correlation_matrix 1 year lag](images/correlation_matrix_1yr_lag.png)

![Linear Regression Plot with KDE](images/linear_regression_plot.png)

|  Metric  |  Result  |
|----------|----------|
|  **Slope**  |  363.84  |
|  **Intercept**  |  713.26  |
|  **R-squared**  |  0.14  |
|  **Mean Squared Error (MSE)**  |  2912525.87  |

Our regression model suggests a modest positive linear relationship between lagged global stress severity ('severity_sum_lag1') and UFO sighting counts. The slope of ~364 indicates that, on average, each additional unit of stress severity is associated with an increase of approximately 364 reported UFO sightings in the following year.

However, the model's R-squared value of 0.14 indicates that only about 14% of the variation in sightings can be explained by this variable alone. This is not unexpected, given the complexity of factors influencing public reporting behaviour, such as media, politics, internet culture, and other psychological or social variables not captured in the dataset.

While not a predictive model, this regression helps quantify the correlation we've already observed and reinforces the central hypothesis: that global stress may play a contributing, if not dominant, role in UFO sighting trends.

---

### **H2: Years with higher total stress severity scores are associated with a greater number of UFO sightings.**

**Validation Approach:**

To test this hypothesis, we began by classifying each year in our dataset as either:

- **High Stress** (severity_sum >= 3)
- **Low Stress** (severity_sum < 3)

We then compared the distribution of 'sightings_per_year' between these two groups.

---

!['UFO Sightings Vs Global Stress Groups'](images/ufo_sightings_by_global_stress_group.png)

This plot clearly shows that:

- The **median** number of sightings is higher in High Stress years
- The **spread** of sightings is wider under High Stress conditions
- There are **notable outliers** (such as 7308 sightings in one Low Stress year)

**Summary Statistics:**

| Stress Group  | Count | Mean   | Median | Std Dev | Min | Max  |
|---------------|--------|--------|--------|---------|-----|------|
| **High Stress**   | 18     | 1717.7 | 271.5  | 1967.5  | 27  | 5076 |
| **Low Stress**    | 49     | 946.7  | 214.0  | 1773.2  | 7   | 7308 |

Although the **mean** number of sightings was **higher** in high-stress years, we couldn’t rely solely on descriptive stats, especially given the spread and skew of the data.

---

### Normality Testing:

We used the **Shapiro–Wilk test** to assess the distribution of each group:

- **Low Stress Group p-value**: 0.0000
- **High Stress Group p-value**: 0.0005

Both groups showed significant deviation from normality, ruling out the use of a t-test.

---

### Mann–Whitney U Test:

Given the non-normal distribution of our data, we applied the **Mann–Whitney U Test**:

- **U statistic**: 562.5  
- **p-value**: **0.087**

---

### Results & Conclusion:

The p-value was **greater than 0.05**, meaning the observed difference in UFO sightings **was not statistically significant** at the 95% confidence level. Therefore, we can not reject the null hypothesis.

That said, the result **hovers close to the significance threshold**, suggesting a **potential trend**. With a larger dataset or additional contextual variables, this hypothesis might gain further support.

For now, however, we **cannot confidently confirm** a statistically significant difference in UFO sightings between high-stress and low-stress years.

---

### **H3: Cultural media events, (such as the release of UFO-themed films or television series) correspond with noticeable short-term spikes in reported sightings.**

**Validation Approach:**

- Flag key media release years in the dataset (e.g., The X-Files in 1993, Independence Day in 1996)
- Visually inspect anomalies in *sightings_per_year* via time-series plots
- Compare spike magnitudes to adjacent years to investigate temporal influence such as lagging. 

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

Due to the absence of meaningful numerical data in our dataset, we had to create additional features in order to prepare for analysis and regression. 

The following features were created:

- **'year'** extracted from the 'datetime' column to serve as a temporal anchor for all analysis.
- **'sightings_per_year'**: A new summary DataFrame was created by grouping the cleaned UFO dataset by 'year', counting the number of sightings annually.
- The global stress dataset was also cleaned:
  - Columns standardised and typed correctly.
  - Aggregated into a yearly summary with:
    - 'stress_event_count' (number of stress events per year)
    - 'severity_sum' (total of severity scores per year).
- Both datasets were filtered to a shared timeframe (1947–2013) and merged using a **left join**, preserving years with zero stress events for baseline comparison.
- Missing values in the merged dataset (due to non-stress years) were filled with '0' to maintain continuity in analysis.

### Exploratory Data Analysis and Regression Summary

Our exploratory phase began with a thorough statistical overview of the dataset, including distributions, outliers, and visual trends. Each key variable (UFO sightings, stress event count, and severity) was examined individually and in relation to one another using line plots, boxplots, and correlation matrices.

From there, we tested whether a simple correlation existed between global stress severity and the number of reported sightings per year. Initial results showed a weak-to-moderate positive correlation. However, by introducing a 1-year lag to the stress variables — to account for potential delay in public psychological response — we saw a noticeable improvement in correlation strength.

This led to the construction of a linear regression model using 'severity_sum_lag1' as a predictor for 'sightings_per_year'. The model confirmed a modest positive relationship, with a slope of approximately 364 — indicating that for each point of increase in stress severity, we might expect an additional 364 sightings the following year.

While the model’s R-Squared score was relatively low (0.14), this is not unexpected given the exploratory nature of the dataset. The regression was not intended for forecasting, but rather to support the hypothesis that societal stress may play a contributing role in increased UFO sighting reports — a theory our analysis consistently reinforced.

## The rationale to map the business requirements to the Data Visualisations
* List your business requirements and a rationale to map them to the Data Visualisations

## Analysis techniques used
* List the data analysis methods used and explain limitations or alternative approaches.
* How did you structure the data analysis techniques. Justify your response.
* Did the data limit you, and did you use an alternative approach to meet these challenges?
### Use of Generative AI in Project Development

Throughout the project, generative AI tools (specifically ChatGPT) were used to support idea development, design thinking, and code optimisation. During the early planning stages, I used AI to help brainstorm a suitable and original concept for the capstone — one that would align with course requirements but still reflect my own interests. This collaborative process helped shape the central hypothesis and business case.

As the project progressed, I used AI to clarify areas I was less confident in — particularly around the more technical elements like regression modelling and interpreting correlation results. It also helped guide the structure of my Jupyter Notebooks and provided feedback on whether certain analytical approaches were appropriate.

In the code itself, I occasionally used AI to review logic, catch errors, and refactor blocks for readability and efficiency. Importantly, I made sure to understand what was being suggested and adapt it to fit my own thinking, rather than copying anything blindly.

Overall, AI tools acted as a supportive co-pilot — helping me stay on track, troubleshoot efficiently, and stay confident during parts of the project that felt outside my comfort zone.


## Ethical considerations

Although this project doesn't involve personal or identifiable data, several ethical considerations were still taken into account during the design and analysis process:

- **Data Source Integrity**: Both datasets used in this project — global UFO sightings (from NUFORC via Kaggle) and the manually curated global stress events — are public and non-sensitive. Care was taken to respect any licensing or attribution where relevant.

- **Anonymity & Privacy**: The UFO dataset contains no personal information, names, or location data beyond city/country-level detail. There is no risk of re-identification.

- **Bias and Interpretation**: This project explores a potentially sensitive cultural phenomenon (UFO sightings) alongside stress events such as wars, disasters, and economic crises. Care was taken not to trivialise or sensationalise these topics. The tone of analysis remains objective, exploratory, and grounded in the data.

- **Causality vs Correlation**: The project avoids making strong causal claims and is transparent about the limitations of correlational methods. The goal is not to prove that stress causes UFO sightings, but to explore possible associations that may be shaped by broader psychological, societal, or media influences.

- **Generative AI Use**: While generative AI tools were used to support planning and code efficiency, all decisions, interpretations, and final outputs reflect the author's own judgement and understanding.

- Approximately 12% of the rows in our UFO dataset were missing a recorded country. While it is technically possible to infer country from latitude and longitude via reverse geocoding, this was not implemented at scale due to performance and ethical limitations around API usage.

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
- Seaborn
- MatPlotLib
- Plotly
- SciPy
- SKLearn



## Credits 

* Code Institute Learning Management System (LMS) for visualisation code,
* https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet for markdown guidance.
* https://en.wikipedia.org/wiki/Kurtosis for clarifying Kurtosis.
* https://www.investopedia.com/terms/p/platykurtic.asp for explaining Platykurtic kurtosis.
* ChatGPT for creating User Story portrait, project title card image, Coding suggestions, project planning ideas, and 'sticking point' clarifications. 
* Copilot for some coding suggestions and code annotation auto-completes. 
* Canva was used for creating the project title card and Persona Card. 
### Content 

- The text for the Home page was taken from Wikipedia Article A
- Instructions on how to implement form validation on the Sign-Up page was taken from [Specific YouTube Tutorial](https://www.youtube.com/)
- The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

- The photos used on the home and sign-up page are from This Open-Source site
- The images used for the gallery page were taken from this other open-source site



## Acknowledgements (optional)
* Thank the people who provided support through this project.
