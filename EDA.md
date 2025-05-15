Chemical Determinants of Wine Quality: A Data-Driven Analysis Using the UCI Wine Dataset
================

## 1. Business Understanding

In this project, the objective is to identify the chemical characteristics that influence wine quality. A wine producer has asked for help in understanding what factors contribute to a good quality wine, using data from the UCI Wine Quality Dataset. Wine quality is typically assessed by trained sensory analysts and can depend on several chemical features such as acidity, alcohol content, sugar levels, and sulfur dioxide levels.

Based on background research and intuition, I hypothesize that features like higher alcohol content and balanced acidity levels may correlate positively with better wine quality. On the other hand, extremely high levels of certain components like sulfur dioxide may negatively affect taste and thus reduce quality. Through exploratory data analysis and statistical testing, I aim to extract non-obvious insights about what makes a wine “good” or “bad” according to the dataset.

## 2. Data Understanding

In this section, we load the red wine dataset and explore its structure.

<img src="figures/Table1-1.png" style="display: block; margin: auto;" />

<img src="EDA_files/figure-gfm/Table2-1.png" style="display: block; margin: auto auto auto 0;" />

The columns of the wine dataset represent a mix of physicochemical properties and a sensory-based quality score. Most features, such as fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, and alcohol, are continuous numerical variables measured on a ratio scale. These values have a true zero and support meaningful arithmetic operations, making them suitable for statistical modeling and correlation analysis. The final column, quality, is a subjective score assigned by wine tasters on a scale from 0 to 10. This variable is ordinal, as it reflects a ranked assessment of wine quality but does not guarantee equal intervals between score values.

<img src="EDA_files/figure-gfm/Table3-1.png" style="display: block; margin: auto;" /> 
For white wine , we can visualize the first few enties

<img src="EDA_files/figure-gfm/Table4-1.png" style="display: block; margin: auto;" />

## 3. Exploratory Data Analysis

From the full set of chemical features in the wine dataset, five were selected for focused analysis: alcohol, volatile acidity, sulphates, residual sugar, and pH. These features were chosen based on a combination of domain relevance, hypothesized impact on sensory perception, and statistical potential to influence quality. Alcohol and volatile acidity are well-known to directly affect aroma, balance, and taste, making them primary suspects in driving wine ratings. Sulphates play a key role in preservation and microbial stability, especially important in white wines. Residual sugar and pH, while more stylistic, influence sweetness and acidity—two central elements in the overall flavor profile.

To explore and compare the red and white wine datasets, we begin by posing several guiding questions and hypotheses. Alcohol is a key factor in determining the body and perceived strength of wine, and different fermentation practices or grape varietals could result in differences in alcohol levels. A histogram allows us to visualize the shape, central tendency, and spread of alcohol content within each wine type, helping us assess whether there is a notable difference in average alcohol levels or variability between red and white wines. We assume that White wines have a higher average alcohol content than red wines.

<img src="EDA_files/figure-gfm/Hist_Alcohol-1.png" style="display: block; margin: auto;" /> 
The distribution of alcohol content differs noticeably between red and white wines. White wines tend to have a wider range and slightly higher average alcohol levels, often peaking around 10.5% to 11.5%, while red wines cluster more tightly around 9.5% to 10.5%. Both distributions are right-skewed, meaning that a small number of wines have significantly higher alcohol content than the average. This suggests that while most wines fall within a moderate alcohol range, white wines are more likely to include higher-alcohol varieties, which may influence perceived sweetness and quality.

Next lets look at the distribution of ph levels.Since acidity plays a significant role in wine freshness and microbial stability, and white wines are typically crafted to retain more acidity, we expect them to have a lower pH. The histogram helps us determine whether pH is a useful discriminating factor between red and white wines, and whether the differences in acidity are substantial enough to consider in quality evaluation or classification.
<img src="EDA_files/figure-gfm/Hist_pH-1.png" style="display: block; margin: auto;" /> 
The distribution of pH values reveals notable differences between red and white wines. White wines generally exhibit lower pH values, indicating higher acidity, with the bulk of observations falling between 3.0 and 3.3. In contrast, red wines tend to have higher pH values, mostly in the range of 3.3 to 3.5, reflecting lower acidity. Both distributions are relatively unimodal and slightly skewed left, though white wine pH has a sharper peak, suggesting more consistency in acidity levels. These pH differences align with winemaking practices: white wines are often preserved with higher acidity for freshness, while red wines undergo longer fermentation and aging, allowing for a higher pH.

Another important factor is the resudual sugar distribution.Residual sugar affects the sweetness and mouthfeel of wine. By plotting a histogram of residual sugar, we aim to test whether white wines tend to be sweeter — either by design (e.g., producing off-dry styles) or due to fermentation control. This plot helps visualize skewness (especially in white wines), identify outliers, and compare sugar levels between the two types.
<img src="EDA_files/figure-gfm/Hist_ResidualSugar-1.png" style="display: block; margin: auto;" /> 
The distribution of residual sugar is markedly different between red and white wines. White wines exhibit a wider and more positively skewed distribution, with most values clustered between 1 and 6 g/dm³, but with a long right tail extending beyond 20 g/dm³. This suggests that some white wines retain significant sweetness, which may reflect stylistic choices such as producing off-dry or semi-sweet varieties. In contrast, red wines have a tighter, more symmetrical distribution, mostly concentrated below 4 g/dm³, indicating drier profiles with less residual sugar overall. The presence of high-sugar outliers in white wines may influence perceptions of sweetness and balance, and could also affect correlations with density, alcohol, and quality.

<img src="EDA_files/figure-gfm/Hist_VolatileAcidity-1.png" style="display: block; margin: auto;" /> <img src="EDA_files/figure-gfm/Hist_Sulphates-1.png" style="display: block; margin: auto;" /> 
Sulphates play a critical role in winemaking as preservatives that help prevent oxidation and microbial spoilage, which can directly affect wine stability and shelf life. Because of this, we are interested in understanding how sulphate concentrations vary between red and white wines. Our hypothesis is that white wines contain higher levels of sulphates than red wines, due to their increased sensitivity to spoilage and the need for freshness preservation. To test this, we use a histogram, which allows us to examine the full distribution of sulphate levels across both wine types, The histogram shows that white wines generally have higher sulphate concentrations than red wines, with peaks around 0.5 to 0.6 g/dm³. In contrast, red wines tend to cluster around lower sulphate values, typically between 0.3 and 0.5 g/dm³. This suggests that sulphates are used more intensively in white wines, likely due to their role in preserving freshness and microbial stability, which are more critical in lighter, more delicate wine styles. <img src="EDA_files/figure-gfm/Boxplot_Quality-1.png" style="display: block; margin: auto;" /> 
The box plot comparing wine quality scores for red and white wines reveals subtle but meaningful differences. Both types have quality ratings that generally range from 3 to 8, but white wines show a slightly higher median score and a narrower interquartile range (IQR), suggesting more consistency in quality. Red wines, while overlapping in score range, display greater variability and more visible outliers on the lower end, indicating occasional lower-quality batches.

To better understand what influences the perceived quality of wine, it is essential to examine how key chemical properties relate to wine quality scores. Variables such as alcohol content, volatile acidity, sulphates, and residual sugar are known to impact the sensory profile and overall acceptability of wine. By analyzing their correlation with quality, we aim to identify which factors most strongly predict or affect wine quality, and whether these relationships differ between red and white wine. These insights not only inform our statistical modeling strategies but also deepen our understanding of the underlying chemistry that distinguishes higher-quality wines from lower-rated ones.

<img src="EDA_files/figure-gfm/Correlation_Boxplots_All-1.png" style="display: block; margin: auto;" /><img src="EDA_files/figure-gfm/Correlation_Boxplots_All-2.png" style="display: block; margin: auto;" /><img src="EDA_files/figure-gfm/Correlation_Boxplots_All-3.png" style="display: block; margin: auto;" /><img src="EDA_files/figure-gfm/Correlation_Boxplots_All-4.png" style="display: block; margin: auto;" /><img src="EDA_files/figure-gfm/Correlation_Boxplots_All-5.png" style="display: block; margin: auto;" /> 

The boxplotS show a positive relationship between alcohol content and quality for both red and white wines. Higher quality scores are associated with higher median alcohol levels, particularly evident in white wines. This suggests that alcohol is a strong indicator of quality, likely because it reflects better fermentation control and riper grapes.They also reveal a slight negative trend for pH, where higher-quality wines tend to have slightly lower pH values, indicating more acidity. This pattern is more evident in white wines, which are generally more acidic. However, the relationship is relatively weak, suggesting pH alone is not a strong determinant of perceived quality.

Sulphates show a mild positive trend with quality, with slightly higher values seen in better-rated wines. The relationship is more visible in white wines, where higher quality levels have increased sulphate concentrations. This could suggest that sulphates, which act as preservatives, may contribute to improved stability and quality perception.

There is a negative association between volatile acidity and quality, especially for red wines. Wines with lower quality scores tend to have higher volatile acidity, which decreases steadily as quality improves. This supports the idea that high volatile acidity — often linked to spoilage — negatively impacts the sensory appeal of wine. The relationship between residual sugar and quality is less clear and inconsistent across wine types. White wines display more variation in sugar levels, but high residual sugar does not consistently align with high or low quality scores. This indicates that residual sugar is not a strong standalone predictor of wine quality and may reflect stylistic preferences rather than objective quality.

Lets run some statistical test on our data. Most of our data is not normally distributed but let’s run a shapiro-wilk test to prove this.
<table class="table table-striped table-hover table-condensed" style="color: black; width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
Shapiro-Wilk Normality Test for Red and White Wine Features
</caption>
<thead>
<tr>
<th style="text-align:left;">
Feature
</th>
<th style="text-align:right;">
Shapiro_Red_p
</th>
<th style="text-align:right;">
Shapiro_White_p
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
alcohol
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
volatile.acidity
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
sulphates
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
residual.sugar
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
pH
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>

The Shapiro-Wilk normality tests revealed that most of the selected chemical features—such as volatile acidity, residual sugar, and sulphates—deviate significantly from a normal distribution in at least one of the wine types, as indicated by p-values below 0.05. These results suggest the use of non-parametric test like the Kendall’s rank correlation test.

<table class="table table-striped table-hover table-condensed" style="color: black; width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
Kendall’s Rank Correlation Test Between Wine Features and Quality
</caption>
<thead>
<tr>
<th style="text-align:left;">
Feature
</th>
<th style="text-align:right;">
Kendall_tau
</th>
<th style="text-align:right;">
Kendall_p
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
alcohol
</td>
<td style="text-align:right;">
0.3524
</td>
<td style="text-align:right;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
volatile.acidity
</td>
<td style="text-align:right;">
-0.1991
</td>
<td style="text-align:right;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
sulphates
</td>
<td style="text-align:right;">
0.0237
</td>
<td style="text-align:right;">
0.0132
</td>
</tr>
<tr>
<td style="text-align:left;">
residual.sugar
</td>
<td style="text-align:right;">
-0.0131
</td>
<td style="text-align:right;">
0.1688
</td>
</tr>
<tr>
<td style="text-align:left;">
pH
</td>
<td style="text-align:right;">
0.0252
</td>
<td style="text-align:right;">
0.0082
</td>
</tr>
</tbody>
</table>

The Kendall’s rank correlation test revealed that among the five chemical features tested, alcohol content had the strongest positive association with wine quality, indicating that as alcohol levels increase, so does the likelihood of receiving a higher quality rating. This finding reinforces previous insights from Spearman correlation and boxplots, confirming that alcohol is a key predictor of wine quality across both red and white wines. Sulphates also showed a modest but statistically significant positive relationship with quality, suggesting that controlled use of sulphur compounds may contribute positively to sensory perception, particularly by preserving freshness.

On the other hand, volatile acidity exhibited a negative correlation with wine quality, consistent with the idea that higher levels—often linked to spoilage—diminish a wine’s appeal. The relationships for residual sugar and pH were weaker and less consistent, indicating that these features, while chemically important, do not have a strong monotonic influence on how quality is rated by sensory analysts. Overall, Kendall’s tau helped confirm the direction and significance of key quality-related trends, particularly in cases where data contained ties or skewness, making it a robust complement to the other non-parametric tests used in this study.

## 4. FINDINGS

The results of our analysis highlight several chemical properties that are meaningfully associated with wine quality, as rated by trained sensory analysts. Among these, alcohol content demonstrated the strongest positive correlation with quality based on Kendall’s rank correlation test, confirming that wines with higher alcohol levels tend to receive better quality scores. This supports the hypothesis that alcohol, as a marker of fermentation completeness and grape ripeness, plays a central role in shaping a wine’s perceived strength and balance. Sulphates also showed a modest but statistically significant positive relationship with quality, suggesting that when used in controlled amounts, they can contribute to wine stability and preservation without negatively affecting taste.

Conversely, volatile acidity was negatively correlated with quality, reinforcing its role as a spoilage indicator that detracts from overall flavor and aroma. The results for residual sugar and pH showed only weak correlations, indicating that these factors are more related to stylistic variation than to perceived quality. The use of Kendall’s tau was especially valuable in this context, as it provided a robust non-parametric measure of association that accounts for ties and non-linear relationships within the data. Overall, the findings confirm that alcohol, volatile acidity, and sulphates are the most influential chemical properties in determining wine quality in this dataset.

## 5. DEPLOYMENT

For a wine business starting out, these findings provide a clear, evidence-based strategy for improving product quality, optimizing production, and building a competitive brand. The analysis shows that alcohol content is one of the strongest predictors of wine quality, so the business should prioritize controlling fermentation processes to ensure wines consistently reach the optimal alcohol range. At the same time, volatile acidity must be carefully managed, as high levels are associated with lower quality scores. This requires investment in clean fermentation practices and routine chemical monitoring.

Sulphates, when used appropriately, serve as effective preservatives that can enhance freshness and contribute positively to perceived quality—particularly in white wines. Therefore, managing sulphate levels within a favorable range can improve shelf-life without compromising taste. While residual sugar and pH are less directly tied to quality scores, they are valuable in shaping the stylistic profile of wines and can be adjusted to suit consumer preferences or brand positioning.
