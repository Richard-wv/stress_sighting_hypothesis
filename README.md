# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

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
* Describe your business requirements


## Hypothesis and how to validate?
* List here your project hypothesis(es) and how you envision validating it (them) 

## Project Plan
* Outline the high-level steps taken for the analysis.
* How was the data managed throughout the collection, processing, analysis and interpretation steps?
* Why did you choose the research methodologies you used?

## The rationale to map the business requirements to the Data Visualisations
* List your business requirements and a rationale to map them to the Data Visualisations

## Analysis techniques used
* List the data analysis methods used and explain limitations or alternative approaches.
* How did you structure the data analysis techniques. Justify your response.
* Did the data limit you, and did you use an alternative approach to meet these challenges?
* How did you use generative AI tools to help with ideation, design thinking and code optimisation?

## Ethical considerations
* Were there any data privacy, bias or fairness issues with the data?
* How did you overcome any legal or societal issues?

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
### Heroku

* The App live link is: https://YOUR_APP_NAME.herokuapp.com/ 
* Set the runtime.txt Python version to a [Heroku-20](https://devcenter.heroku.com/articles/python-support#supported-runtimes) stack currently supported version.
* The project was deployed to Heroku using the following steps.

1. Log in to Heroku and create an App
2. From the Deploy tab, select GitHub as the deployment method.
3. Select your repository name and click Search. Once it is found, click Connect.
4. Select the branch you want to deploy, then click Deploy Branch.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click now the button Open App on the top of the page to access your App.
6. If the slug size is too large then add large files not required for the app to the .slugignore file.


## Main Data Analysis Libraries
* Here you should list the libraries you used in the project and provide an example(s) of how you used these libraries.


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
