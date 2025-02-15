# Week 1
### Basic visualisation methods
#### Pie Chart
**Problems**
- Readers struggle to judge relative sizes of pie slices
- aren't efficient in data-to-ink/pixel ratio
- hard to pull off - colours need to have high contrast, labels need to be carefully placed and not overlap
#### Pareto Chart
- special type of bar chart where values being plotted are arranged in descending order
- developed to illustrate the Pareto 80-20 rule
#### Lorenz Curve
- line graph specially designed to represent the cumulative distribution function of the empirical probability distribution of a measure such as income or wealth
![](images/Pasted%20image%2020240222141207.png)
## Correlation Analysis Best Practices
- Remove fill colour to reduce over-plotting
- Visually distinguishing datasets when divided into groups
- Using trend line to enhance perception of a correlation's shape, strength, and outliers
- Using multiple trend lines to see categorical differences
- Optimise aspect ratio and quantitative scales
- Removing the rough to see the smooth more clearly
- Use trellis to reduce complexity and over-plotting
- Using reference lines to enhance comparison between scatterplots
### Table Lens
A table lens provides a simple way to look for correlations among two or more variables all at once. It uses horizontal bars to encode values, arranged like a table, with a separate column for each variable, and a separate row for each item that has been measured
# Week 2
### Perception
Perception is the organisation, identification, and interpretation of sensory information in order to represent and understand the environment
**Graphical Perception** refers to the ability of viewers to interpret visual (graphical) encodings of information and thereby decode information in graphs
### Change Blindness
- phenomenon of visual attention in which changes to a visual scene may go unnoticed under certain circumstances, despite being clearly visible and possibly even in an attended location
- make changes visible in visualisations to reduce the cognitive load
- visualisation serves as an external aid to augment working memory
### Signal Detection
#### Just Noticeable Difference (JND)
**JND (Weber's Law)**
	$\qquad$$$\begin{flalign}Perceived\ change = k\cdot\frac{\Delta I}{I} &&\end{flalign}$$$$\begin{flalign}, \ where\ k=Scale\ Factor,\ \Delta I=Change\ of\ Intensity,\ I=Physical\ Intensity&&\end{flalign}$$
- ratios more important than magnitude
- most continuous variation in stimuli are perceived in discrete steps
#### Encoding data with Colour
- Value is perceived as ordered
	- For encoding ordinal and continuous (not as well) variables
- Hue is normally perceived as unordered
	- Encode nominal variables using colour
### Magnitude Detection
#### Steven's Power Law
$\qquad$$$\begin{flalign}S = I^p, \ where\ S=Perceived\ Sensation,\ I=Physical\  Intensity,\ p=Exponent&&\end{flalign}$$
- predicts bias, not necessarily accuracy
### Pre-attentive Processing
- A limited set of visual properties are processed pre-attentively (without need for focusing attention)
- Pre-Attentive: immediately recognise variation with little or no conscious effort (<200 or 250ms)
- Attentive: takes some deliberate effort to perceive differences
- **Spatial conjunctions** are often pre-attentive:
	- Motion and 3D disparity 
	- Motion and colour
	- Motion and shape
	- 3D disparity and colour
	- 3D disparity and shape
- **But most conjunctions are NOT pre-attentive**
### Gestalt Grouping
- [Gestalt Grouping](https://www.toptal.com/designers/ui/gestalt-principles-of-design#:~:text=In%20gestalt%2C%20similar%20elements%20are,each%20other%20in%20a%20design.) 
- provides high-level guidelines on grouping
# Week 3
### Graphical Integrity
- Graphics must not quote data out of context
	- Show the entire scale
- Visual attribute value should be directly proportional to data attribute value
	$\qquad$$$\begin{flalign}Lie\ factor = \frac{size\ of\ effect\ shown\ in\ graphic}{sizes\ of\ effect\ in\ data}&&\end{flalign}$$$$\begin{flalign}Size\ of\ effect = k\cdot\frac{\Delta I}{I}&&\end{flalign}$$
	$Truth = 1.0$
- Avoid using two or three varying dimensions to show on-dimensional data
### Data-ink Ratio  Maximisation
- Data-ink is the non-erasable ink for the presentation of data
- Reduce the non-data-ink (a.k.a., chartjunk)
	- Remove the unnecessary non-data-ink
	- Emphasise data-ink
- Enhance the data-ink
	$\qquad$$$\begin{flalign}\frac{Data\ Ink}{Total\ Ink}=Data\ Ink\ Ratio&&\end{flalign}$$
#### ChartJunk
- Avoid using unnecessary colour shading for the bar
- Avoid colourful or wallpaper background
- Avoid using 3D effects in graphics
### Rules for Encoding Values in Graph
1. Avoid using point alone to display time-series data
	 ![](images/Pasted%20image%2020240222140830.png)
2. Avoid using points to represent discrete values
	![](images/Pasted%20image%2020240222140855.png)
3. Bars don't work unless the quantitative scale begins at zero
	![](images/Pasted%20image%2020240222140928.png)
### Practical Guides for Using Colour in Charts
1. Make sure that the background - the colour that surrounds them - is consistent
2. Use a background colour that contrasts sufficiently with the object
3. Use colour only when needed to serve a particular communication goal
4. Use different colours only when they correspond to different meanings in the data
5. Use soft, natural colours to display most information and bright/or dark colours to highlight information that requires greater attention
6. Stick with a single hue and vary intensity from pale colours for low values to increasingly darker and brighter colours for high values, i.e. use [sequential colormap](sequential%20colormap)
### Graph notations 
- Should not manipulate the aspect ratio to intentionally exaggerate or downplay the rate of change
- Stick to the convention of making your graphs wider than they are tall
- Orientation of label should be reader friendly
### Other Tips
- Focus on a few key stories that will resonate with your audience, and design graphs that help you tell those stories
- Accurately represent the data by including the data source
- Avoid what Tufte calls "chart junk" which is ornamentation that does not show data such as clip art
# Week 10: Hierarchical Data Visualisation
### Hierarchical Data
- focuses on the hierarchical relationship between objects
