Name: Sandesh Adhikary
NETID: adhikary

## The Question

With the data provided, I was interested in visualizing how much truth there is to the notion that Seattle is one of the gloomiest cities in the US (when it comes to sunshine). My goal in this project is to visualize the relative lack/abundance of sunshine in Seattle compared to a few other major cities spanning the four quadrants and distributed along the coasts of the US. A possible use case might be for a viewer thinking of moving from Seattle to a different city in search of sunshine. This person has a few cities in mind, and wants information relative to their current location (Seattle).

## The Data
The raw data consists of geographic information (city, latitude, longitude), temporal information (month, mothnum), and hours of sunshine per month (averaged over 1981-2010). I also extracted an additional field 'average high temperature' from usclimatedaa.com. My intuition here was to contextualize sunshine-hours with the temperature -- what use is a sunny day if it's too hot to go out?

I applied the following three data transformations:
	
	1. Converted average sunshine-hours to average _daily_ sunshine hours since the total sunny hours in a month was not an intuitive metric. Using the linearity of simple averages, I computed the mean daily sunshine hours averaged between 1981-2010 by dividing the avg. sunshine hours field by 24.

	2. Binned average high temperatures into 4 bucket since viewers cannot really processes small differences in continuous gradients or when there are too many categorical bins. I adapted the temperature categorization from the Universal Thermal Climate Index, which segments temperatures on the basis of physiological stress caused to humans. I'm using these as a proxy for thermal-comfort levels. The actual UTCI is more granular than the 5 bins I have used, and is defined with respect a "standard" human and reference environment. 

	3. Faceted the data by city, and sorted by month. The faceting was to focus on individual comparisons with Seattle, the sorting was to introduce additional context related to seasons.

## Visualization Encodings
The main element in my visualization is the radial plot, which encodes information about seasons, temperature, average daily sunshine hours, and avg. daily sunshine hours relative to Seattle. I chose a circular plot as it allowed me to better encode the cyclic nature of seasons, which I believe provides a lot of context. The secondary element in my visualization is the underlying map of the US, which provides geographic context (e.g. Miami's hot summers make more sense when you recall it's in the southern tip)

Here are the visual encodings I have used in terms of their importance:
	1) Average daily sunshine hours: This is encoded by the height of the yellow filled-arcs within each plot, defined with a true zero (at the origin) and a max of 12 hrs. I treated the data as quantitative and used a linear scale mapping the domain [0,24] to radii pixels [0,480].
	Note that this information is solely encoded in the height of the arcs, and not in angular differences.
	2) Average daily sunshine hours relative to Seattle: In each plot, I have included purple outlines of the avg. daily sunshine hours for Seattle.
	3) Temporality/Seasonality: For each radial plot, the outer-most ring tells us to what month (ordinal data) each angular section corresponds. Since all months occupy the same angle, we are not relying on the viewer to parse relative differences in angles (which is a common problem with radial plots)
	4) Average daily high temperature: I used an ordinal categorical color scheme for the UTCI temperature bins. I aimed at picking colors that intuitively depict warm (red) and cold (blue) temperatures, with green representing the sweet spot in the middle.
	5) Geographic information: I mapped the latitude/longitude of each city onto a map of the US using the AlbersUSA projection, an equal area conic projection specific to the continental USA. My focus in the geographic encoding was more to highlight the general quadrant and location (e.g. coastal versus non-coastal) so the AlbersUSA projection works fine in this regard (e.g. I'm not trying to exactly map distances between cities)
	6) Colors: I have tried to use either black or gray for any non-color coded elements. The background color (gray) is muted to highlight data-specific colors.

## Weaknesses:
Here are some of the weaknesses of my visualization that I am aware of:
	1) The radial plots make it a bit difficult to discern exact values of avg. sunshine, and also to compare between non-neighboring plots. My hope is that the addition of the grid lines minimizes these problems.
	2) The temperature bins obscure small differences. For example, 79 degrees is considered "just right" but a single degree increase is not. This is a by-product of minimizing the number of categories, and would likely emerge with any binning scheme.
	3) It is not easy to compare cities that aren't Seattle. This was a by-product of trying to keep things Seattle-centric. I think an interactive version of this viz might solve this problem a bit i.e. the user getting to pick which city to keep as the reference point.
	4) Unused space in the middle. I could probably add 1-2 additional cities to make better use of the space








