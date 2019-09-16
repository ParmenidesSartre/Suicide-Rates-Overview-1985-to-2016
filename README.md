# Suicide Rates Overview 1985 to 2016
![Suicide is never worth it](https://www.standardmedia.co.ke/evemedia/eveimages/monday/mrsxszchsjcdcjizop5b962a4a840de.jpg)

Suicidal ideation is not something should be regarded as something that is normal. For some , it is a cry for help which should be answered. Suicide is devastating and the effects of suicide on family members and loved ones of the person who has died by suicide can be severe and far-reaching.

## Data

The data was taken from the '[Global suicide data](https://www.kaggle.com/sathutr/global-suicide-data)' in _[Kaggle](https://www.kaggle.com/)_.

This compiled dataset pulled from four other datasets linked by time and place, and was built to find signals correlated to increased suicide rates among different cohorts globally, across the socio-economic spectrum.
### Columns of dataset :

country, year, sex, age group, count of suicides, population, suicide rate, country-year composite key, HDI for year, gdp_for_year, gdp_per_capita, generation (based on age grouping average).

## References
United Nations Development Program. (2018). Human development index (HDI). Retrieved from [http://hdr.undp.org/en/indicators/137506](http://hdr.undp.org/en/indicators/137506)

World Bank. (2018). World development indicators: GDP (current US$) by country:1985 to 2016. Retrieved from  [http://databank.worldbank.org/data/source/world-development-indicators#](http://databank.worldbank.org/data/source/world-development-indicators#)

[Szamil]. (2017). Suicide in the Twenty-First Century [dataset]. Retrieved from  [https://www.kaggle.com/szamil/suicide-in-the-twenty-first-century/notebook](https://www.kaggle.com/szamil/suicide-in-the-twenty-first-century/notebook)

World Health Organization. (2018). Suicide prevention. Retrieved from  [http://www.who.int/mental_health/suicide-prevention/en/](http://www.who.int/mental_health/suicide-prevention/en/)


# Findings

 ### Which generation has the highest number of suicide rates ?
	 
| Age  Group     | Suicide/100k  |
|----------------|---------------|
| 75+ years      |     23.96     |
| 55 - 74 years  |     16.16     |
| 35 - 54 years  |     14.95     |
| 25 - 34  years |     12.19     |
| 15 - 24 years  |      8.95     |
| 5 - 14 years   |      0.62     |

Conclusion : It seems that people commit suicide more when they are older.

### Connection between GDP and suicide rate for all country in the data set.
```python
def create_df(country):
    df = data[data['country'] == country].groupby('year').sum()
    return df

def calculate_corr(df):
    return df['easy_gdp_cal'].corr(df['suicides/100k pop'])

correlation = {}
for country in data['country'].unique():
    corr = calculate_corr(create_df(country))
    correlation[country] = corr

li = []
for key,value in correlation.items():
    if value < -0.3:
        li.append(key)
        
        
sad = []
for key,value in correlation.items():
    if value > 0.3:
        sad.append(key)
        
print("""It seems that only {} % of the country shows a decrease in number of suicides due to improvement in living condition.There must be other reason such cultural, war (which should be explainable by low gdp) or various other factors.""".format(round(len(li)/data['country'].nunique() * 100),2))
print()
print("""It seems that only {} % of the country shows an increase in number of suicides due to improvement in living condition.There must be other reason such cultural, war (which should be explainable by low gdp) or various other factors.""".format(round(len(sad)/data['country'].nunique() * 100),2))
print()
print('27 % of countries is neutral')
```
Conclusion :
It seems that only 56 % of the country shows a decrease in number of suicides due to improvement in living condition.There must be other reason such cultural, war (which should be explainable by low gdp) or various other factors.

It seems that only 17 % of the country shows an increase in number of suicides due to improvement in living condition.There must be other reason such cultural, war (which should be explainable by low gdp) or various other factors.

27 % of  the countries is neutral.


### Suicide rate among first world country through the years.
![Suicide rate](https://github.com/ParmenidesSartre/Suicide-Rates-Overview-1985-to-2016/blob/master/Comparison%20of%20Suicide%20Rate%20among%20First%20World%20Country.png)
