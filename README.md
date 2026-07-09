# Could This Multi-Billion Dollar City Fund Save Chicago Schools?

*An analysis of Tax Increment Financing (TIF) across all 77 Chicago neighborhoods*

By Giovanni Del Angel · [LinkedIn](https://www.linkedin.com/in/giovannidelangel) · [Tableau Public Interactive Dashboard](https://public.tableau.com/app/profile/giovanni.del.angel/viz/ChicagosEducationFundingAnalysis/EducationDashboard)
## Executive Summary
Chicago has collected $2.97B through Tax Increment Financing (TIF), a local government tool meant to fund public improvements. Yet few people ask whether this money is reaching the neighborhoods where its impact would be felt the most. To see where these public funds are allocated relative to the neighborhoods that need them, this report analyzed public data collected across all 77 Chicago neighborhoods. Three tools are utilized in the data analysis. Python pulled public data on the City of Chicago to determine how much TIF funding is allocated to each Chicago neighborhood. SQL identified the neighborhoods where the reallocation of these public funds would make the greatest impact. Tableau visualized the insights in an interactive dashboard. The findings are striking, though not surprising given Chicago's long history of inequity. It was evident that these public funds are not where they need to be. For instance, the Loop has collected $345M in TIF funding while the South Side neighborhood of Riverdale has collected just over $1M. Roughly 60% of all TIF funding sits in neighborhoods where it is needed the least. A need-based surplus would channel millions of dollars into Chicago’s most impoverished neighborhoods, all from existing public funds. No new taxes needed.

## How the Money Works
Every year, the City of Chicago allocates public funds collected from rising property taxes through a local government program called Tax Increment Financing (TIF). The program is simple. When a specific area is designated a TIF district, the growth in its property tax revenue is used to fund improvements to schools, parks, and other local infrastructure. Over time, these public funds have grown significantly. Today, the City of Chicago has collected a staggering $2.97B in TIF funding.

Typically, the conversations around the quality of education in Chicago's impoverished neighborhoods stop at what is already clear to the residents who live there. Some neighborhoods in Chicago are far better off than others. Most Chicagoans can see this every day, but identifying the problem does not solve it. With that in mind, a more useful question is worth posing. Is there public funding already being collected that could be channeled to the Chicago neighborhoods that need it most? To answer it, this report compared TIF funding across all 77 Chicago neighborhoods to each neighborhood's calculated level of need.

## Key Findings
The analysis began with public data collected from the Chicago Data Portal, accessed via the city's Socrata API, which offers programmatic access to thousands of public datasets from governments and organizations worldwide. Four key datasets formed the foundation. The first mapped the boundaries of all 77 Chicago neighborhoods. The second contained each neighborhood's Hardship Index, a single score that combines six measures of hardship: unemployment, age dependency, education, per capita income, crowded housing, and poverty. It consolidates these into a single number, allowing for comparison across neighborhoods, where a higher score indicates greater need. The third mapped the boundaries of the city's TIF districts, totaling more than 100. The fourth reported the amount of public funding collected in each TIF district. Together, these sources covered every neighborhood in Chicago and the $2.97 billion in TIF funding collected.

The main challenge was that Chicago neighborhoods do not align perfectly with TIF district boundaries. A single TIF district can span multiple neighborhoods. To calculate public funding per neighborhood, Python was used with the pandas and geopandas libraries to perform a spatial join based on areal overlap. For each TIF district, the analysis measured the extent to which it overlapped each neighborhood and allocated its funding accordingly. This process also involved reconciling the names of more than 100 TIF districts across two datasets that did not exactly match, using a combination of Python scripts and manual review to ensure accuracy.

Once each neighborhood was assigned its share of public funding, the next step was to compare need directly with funding. This comparison is complicated because need is measured on a scale of 0 to 100, while funding is expressed in dollars, making direct comparison impossible. To address this, both metrics were converted into z-scores, a standard method that expresses each value as the distance above or below the citywide average. This placed need and funding on a comparable scale. TIF dollars presented a second challenge: a few downtown districts hold hundreds of millions, while most hold almost nothing, which can skew comparisons. To mitigate this, a log transformation was applied to reduce the impact of extreme values. With both measures on the same scale, each neighborhood received a mismatch score that represented the gap between its level of need and its funding. A high mismatch indicates a high need with low funding. From there, SQL queries run through DuckDB identified neighborhoods most in need and analyzed the concentration of funding. Tableau integrated these findings into an interactive dashboard.

Three key findings emerged. First, TIF funding does not follow need. Plotting each neighborhood's need against its TIF funding shows a negative slope, meaning that as need increases, public funding decreases. If funds were accurately aligned with need, the trend would be upward, but instead, it drops, indicating that TIF funding is not reaching Chicago neighborhoods that need it most. Second, funding is concentrated in the city's wealthiest areas, primarily downtown and North Side neighborhoods, which have the least need. About 60% of TIF money goes to neighborhoods with below-average need. The Loop, one of the wealthiest neighborhoods, received $345 million in TIF funding, while many others received a fraction of that. Conversely, Riverdale on the South Side, an area with significant needs, received just over $1 million. Third, neighborhoods with the greatest need are mainly located on the South and West Sides. The list of most under-resourced neighborhoods, exhibiting high need and low funding, consists entirely of areas from these regions.

## Key Visuals

[Tableau Public Interactive Dashboard](https://public.tableau.com/app/profile/giovanni.del.angel/viz/ChicagosEducationFundingAnalysis/EducationDashboard)

TIF Accumulation vs. Neighborhood Hardship
![Need Vs. Money Scatter](Need%20Vs.%20Money%20Scatter.png)

Geographic Distribution of Money and Need
![Neighborhoods Map](Neighborhoods%20Map.png)

10 Most Under-Resourced Neighborhoods
![Under-Resourced Neighborhoods](Under-Resourced%20Neighborhoods.png)

## A Solution Within Reach
When the City of Chicago implemented its Tax Increment Financing (TIF) program, the idea was well-intentioned. The goal was to make much-needed improvements to neighborhoods across the city. As it currently operates, the program unfortunately invests the majority of its public funding in the neighborhoods that need it the least. Chicago's most impoverished neighborhoods see little to no improvements to their schools, parks, and other local infrastructure, while the city's most affluent neighborhoods continue to collect millions. At first glance, this may appear to be a lack of public funding, but the numbers tell a different story. Chicago has collected $2.97B in TIF funding. Public funding that could change the lives of millions of disadvantaged residents already exists. It is located in all the wrong places.

Careful analysis of all 77 Chicago neighborhoods revealed that the city's most impoverished neighborhoods are struggling not because of a lack of public funding, but because of how it is distributed. For a city often plagued by negative publicity over how it treats its most underserved residents, this is a significant insight. Chicago lawmakers could make real change now. No new money is needed. No new taxes are needed. A simple reallocation of public funds could change lives today. The real question is why the City of Chicago has not seriously considered it, especially when the option has been on the table for years.

## Recommendations
The City of Chicago has a rarely used but potentially powerful tool known as a Tax Increment Financing (TIF) surplus. When a TIF district accumulates more funds than needed, the city can declare a surplus and return those funds to local neighborhood infrastructure, including Chicago Public Schools, which, by law, would receive about 55%. Proper distribution of this surplus based on need, rather than on where the money sits, could direct hundreds of millions of dollars to the neighborhoods and schools most in need, all without raising taxes. For example, when Chicago recently declared a record surplus of $712M, approximately $392M was allocated to schools. However, this process has limitations. TIF funds cannot be added directly to a school's daily operating budget, as they primarily fund capital projects such as new buildings and repairs. This highlights that the greatest needs are often where resources are lacking, and while TIF surpluses can guide resource allocation, they don't guarantee that every gap will be closed. Ultimately, the resources to do more already exist; the key is whether the city chooses to act and implement these recommendations.

## Setup and Replication
```bash
pip install -r requirements.txt
# Open and Run "Chicago TIF Analysis.ipynb" #
```

## Files
- `Chicago TIF Analysis.ipynb` — Python & SQL Analysis
- `Chicago TIF Data.csv` — Data on Chicago's TIF Districts
- `Community Areas Boundaries.geojson` — Chicago Neighborhood Boundaries
- `Chicago TIF Dashboard.twbx` - Tableau Workbook
- `Dashboard.png` · `Neighborhoods Map.png` · `Need Vs. Money Scatter.png` · `Under-Resourced Neighborhoods.png` — Data Visualizations
