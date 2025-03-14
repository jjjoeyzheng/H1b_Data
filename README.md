Data Access: https://drive.google.com/drive/folders/1NhDtZynEfZZwaODPlX_Pa-S2Fv5XvJMW?usp=drive_link
Data Source: https://flag.dol.gov/programs/lca

Below are the main data cleaning steps implemented in this project:
1. Data Reading and Initial Check：Read CSV files for 2019–2022 using pd.read_csv while addressing mixed data type warnings.

2. Filtering Target Records （H1B application）
- Filter the dataset to include only H-1B applications based on the Visa_Class column.
- For the Case_Status column, retain only the records that indicate certification (using "CERTIFIED" for 2019 and "Certified" for 2020–2022) to ensure only certified applications are analyzed.

3. Handling Missing Values
- Evaluate missing values across columns using methods like df.isna().sum().
- Remove rows with missing values in critical fields (e.g., Employer_Location) to maintain data accuracy for subsequent analysis.

4. Field Extraction and Conversion
- Extract state information from the Employer_Location field (which is formatted as "City, State") using a lambda function (e.g., lambda x: x.split(',')[-1].strip()) and create a new column called State.
- Convert the year column to a string to facilitate proper grouping and animation in the visualization.


Charts Generated:
1. Bar Chart: 2019-2022 H1B Applications, Certified & Approvals
Display content: Shows three key indicators of H1B applications from 2019 to 2022: Total Applications, Certified Applications, and Approvals.
Description: Each indicator is presented in the form of a grouped bar chart, with specific numbers marked above the bar, and detailed information will be displayed when the mouse hovers. This chart intuitively compares the changing trends of each indicator in different years.

2. Pie Charts: 2019-2022 H1B Approvals Proportion by Year
Display content: Shows the ratio of approvals to no approvals in each state (or each year as a whole) in 2019, 2020, 2021, and 2022.
Description: In each chart, different shades of blue are used to represent the Approvals part, while the No Approvals part is represented by light gray; the year and the specific number and ratio of approvals are marked outside the chart to facilitate the comparison of data from each year.

3. Choropleth map made by Folium: certified_h1b_map
Display content: Display the distribution of the number of certified H1B applications in each state on a US map.
Description: By deleting the records with missing Employer_Location in the data, extracting the state name from Employer_Location, and then summarizing the number of certified by state. Use discrete color bands (yellow or blue, optional) and preset intervals (bins) to map the data of each state, and the color depth reflects the number of certified in each state. The state name is displayed when the mouse hovers, so that the specific value of each state can be intuitively understood.

4. Plotly Express Animated Choropleth Map: certified_h1b_map_by_year
Display content: The trend of the number of certified H1B applications in each state from 2019 to 2022 is displayed through animation.
Description: The number of certified in each state is binned (such as: 0-1k, 1k-5k, etc.) and mapped with blue discrete colors. Each frame of the animated map represents a year. Users can observe the time series changes of data in each state by playing the animation, and the specific certified value can be displayed when the mouse hovers.
