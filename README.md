# University Ranking Tracker
A notebook for scraping ranking data from QS, ARWU and TIMES world university and subject rankings.
<br>
**Author:** [Elliott Zhu](https://scholar.google.com/citations?user=Cw5v2f4AAAAJ&hl=en)

## Introduction

This note book creates streamlined process to easily access and scrape university ranking data across three major ranking
systems: Times Higher Education, ARWU and QS. It fully incorporates the dynamic web loading structure: Asynchronous JavaScript
 and XML (AJAX) to extract and compose the published data on corresponding websites. It further provides the accurate computed ranking
 positions given the published ranking methodologies.


-----

## Contributions

Contributions are very welcome. Interested contributors can consult our
[contribution
guidelines](https://github.com/benkeser/survtmle/blob/master/CONTRIBUTING.md)
prior to submitting a pull request.

-----

## Citation

After using the `survtmle` R package, please cite both of the following:

``` 
    @manual{benkeser2017survtmle,
      author = {Benkeser, David C and Hejazi, Nima S},
      title = {{survtmle}: Targeted Minimum Loss-Based Estimation for
               Survival Analysis in {R}},
      year  = {2017},
      howpublished = {\url{https://github.com/benkeser/survtmle}},
      url = {http://dx.doi.org/10.5281/zenodo.835868},
      doi = {10.5281/zenodo.835868}
    }

    @article{benkeser2017improved,
      author = {Benkeser, David C and Carone, Marco and Gilbert, Peter B},
      title = {Improved estimation of the cumulative incidence of rare
               outcomes},
      journal = {Statistics in Medicine},
      publisher = {Wiley-Blackwell},
      year  = {2017},
      doi = {10.1002/sim.7337}
    }
```

-----

## License

© 2017-2020 [Elliott Zhu](https://scholar.google.com/citations?user=Cw5v2f4AAAAJ&hl=en)

The contents of this repository are distributed under the MIT license.
See below for details:

    The MIT License (MIT)
    
    Copyright (c) 2017-2020 Elliott Jie Zhu
    
    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:
    
    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.
    
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.

## Prerequisites
Please check the Jupyter notebook in this depository for weighting data listed below 
and required packages. 


=== Times Higher Education Subjects ===

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subject</th>
      <th>Page</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Subject.Arts.Humanities</td>
      <td>arts-and-humanities</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Subject.Education</td>
      <td>education</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Subject.Law</td>
      <td>law</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Subject.Psychology</td>
      <td>psychology</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Subject.Business.Economics</td>
      <td>business-and-economics</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Subject.Health</td>
      <td>clinical-pre-clinical-health</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Subject.Computer.Science</td>
      <td>computer-science</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Subject.Engineering.Technology</td>
      <td>engineering-and-IT</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Subject.Life.Sciences</td>
      <td>life-sciences</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Subject.Physical.Sciences</td>
      <td>physical-sciences</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Subject.Social.Sciences</td>
      <td>social-sciences</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === Times Higher Education Weightings (Top 5) ===')
display(weightings['weightings_times'].head(5))
```

    
     === Times Higher Education Weightings (Top 5) ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subjects</th>
      <th>Teaching</th>
      <th>Research</th>
      <th>Citation</th>
      <th>Industry Income</th>
      <th>International Outlook</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>World.University.Rankings</td>
      <td>0.300</td>
      <td>0.300</td>
      <td>0.300</td>
      <td>0.025</td>
      <td>0.075</td>
    </tr>
    <tr>
      <th>1</th>
      <td>World.Reputation.Rankings</td>
      <td>0.300</td>
      <td>0.300</td>
      <td>0.300</td>
      <td>0.025</td>
      <td>0.075</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Subject.Arts.Humanities</td>
      <td>0.374</td>
      <td>0.376</td>
      <td>0.150</td>
      <td>0.025</td>
      <td>0.075</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Subject.Education</td>
      <td>0.327</td>
      <td>0.298</td>
      <td>0.275</td>
      <td>0.025</td>
      <td>0.075</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Subject.Law</td>
      <td>0.327</td>
      <td>0.308</td>
      <td>0.250</td>
      <td>0.025</td>
      <td>0.090</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === ARWU Subjects (Top 5) ===')
display(weightings['subject_arwu'].head(5))
```

    
     === ARWU Subjects (Top 5) ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subject</th>
      <th>Page</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mathematics</td>
      <td>mathematics.html</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Physics</td>
      <td>physics.html</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chemistry</td>
      <td>chemistry.html</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Earth Sciences</td>
      <td>earth-sciences.html</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Geography</td>
      <td>geography.html</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === ARWU Weightings (Top 5) ===')
display(weightings['weightings_arwu'].head(5))
```

    
     === ARWU Weightings (Top 5) ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ranktype</th>
      <th>PUB</th>
      <th>Normalized Citation</th>
      <th>IC</th>
      <th>Number Top10</th>
      <th>Award</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Physics</td>
      <td>100</td>
      <td>100</td>
      <td>20</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chemistry</td>
      <td>100</td>
      <td>100</td>
      <td>20</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mathematics</td>
      <td>100</td>
      <td>100</td>
      <td>20</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Earth Sciences</td>
      <td>100</td>
      <td>100</td>
      <td>20</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ecology</td>
      <td>100</td>
      <td>100</td>
      <td>20</td>
      <td>100</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === QS Weightings (Top 5) ===')
display(weightings['weightings_qs'].head(5))
```

    
     === QS Weightings (Top 5) ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Subject</th>
      <th>Academic</th>
      <th>Citation</th>
      <th>Employer</th>
      <th>h-index</th>
      <th>International Student</th>
      <th>International Faculty</th>
      <th>Faculty Student</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Accounting.Finance</td>
      <td>0.5</td>
      <td>0.10</td>
      <td>0.3</td>
      <td>0.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Agriculture.Forestry</td>
      <td>0.5</td>
      <td>0.20</td>
      <td>0.1</td>
      <td>0.20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anatomy.Physiology</td>
      <td>0.4</td>
      <td>0.25</td>
      <td>0.1</td>
      <td>0.25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Anthropology</td>
      <td>0.7</td>
      <td>0.10</td>
      <td>0.1</td>
      <td>0.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Archaeology</td>
      <td>0.7</td>
      <td>0.10</td>
      <td>0.1</td>
      <td>0.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

# Examples
## Times Higher Education

The AJAX logic of [Times Higher Education](http://timeshighereducation.com) is simple and consistent across both the world university ranking and subject
rankings. The current logic works for data ranging from 2011 to 2021. Apply the indicator weighting according to
[Times Higher Education Methodology](https://www.timeshighereducation.com/world-university-rankings/world-university-rankings-2020-methodology)


```python
#Define times scraping function
def fetch_TIMES(rank=None, year=None, weightings=weightings['weightings_times'],page =weightings['subject_times'] ):
        if 'Subject' in rank:
            page = page[page.Subject == rank].Page.reset_index(drop=True)[0]
            url1 = "https://www.timeshighereducation.com/world-university-rankings/" + str(
                year) + "/subject-ranking/" + page
        else:
            url1 = "https://www.timeshighereducation.com/world-university-rankings/" + str(year) + "/world-ranking"
        r = requests.get(url1, headers={'User-Agent': 'Mozilla/5.0'})
        soup = BeautifulSoup(r.content, "lxml")
        scripts = soup.find_all('script')
        for script in scripts:
            try:
                if 'jQuery.extend' in script.contents[0]:
                    jsonStr = script.contents[0].split('jQuery.extend(Drupal.settings,')[1]
                    jsonStr = jsonStr.rsplit(');', 1)[0]
                    jsonObj = json.loads(jsonStr)
                    url1 = jsonObj['the_data_rankings']['#datatable-1']['ajax']['url']
            except:
                pass

        req = urllib.request.Request(url1, headers={'User-Agent': 'Mozilla/5.0'})
        with urllib.request.urlopen(req) as url:
            data = json.loads(url.read().decode())
        df = pd.DataFrame(data['data'])
        try:
            df = df[['rank', 'name', 'scores_overall',
                     'scores_teaching', 'scores_research', 'scores_citations',
                     'scores_industry_income', 'scores_international_outlook',
                     'location', 'stats_number_students', 'stats_student_staff_ratio',
                     'stats_pc_intl_students', 'stats_female_male_ratio']]
            df.columns = ['Rank', 'University', 'TotalScore',
                          'Teaching', 'Research', 'Citation',
                          'Industry Income', 'International Outlook',
                          'Country', 'Student Count', 'Faculty/Student',
                          'International Student%', 'Female/Male']
        except:
            df = df[['rank', 'name', 'scores_overall',
                     'scores_teaching', 'scores_research', 'scores_citations',
                     'scores_industry_income', 'scores_international_outlook',
                     'location']]
            df.columns = ['Rank', 'University', 'TotalScore',
                          'Teaching', 'Research', 'Citation',
                          'Industry Income', 'International Outlook',
                          'Country']

        weightings = weightings[weightings.Subjects == rank].reset_index(drop=True)

        df = df.replace('-', 0, regex=True)

        df[['Teaching', 'Research', 'Citation', 'Industry Income', 'International Outlook']] = \
            df[['Teaching', 'Research', 'Citation', 'Industry Income', 'International Outlook']].astype('float32')

        df['Calculated Score'] = np.sum(
            np.multiply(df[['Teaching', 'Research', 'Citation', 'Industry Income', 'International Outlook']],
                        weightings[['Teaching', 'Research', 'Citation', 'Industry Income', 'International Outlook']]),
            1)

        df['Calculated Rank'] = df['Calculated Score'].rank(method='min', ascending=False)
        df['Subject'] = rank.replace('.', ' ')
        try:
            df['Subject'] = df['Subject'].str.replace('Subject', '')
        except:
            pass

        df['National Rank'] = df.groupby('Country')['Calculated Score'].rank(method='min', ascending=False)
        df['Top 100'] = df['Calculated Rank'] <= 100
        df['Year'] = year

        return df

def TIMES_rank(years=[2021], ranks=['World.University.Rankings','Classics.Ancient.History']):

    df_TIMES = pd.DataFrame()
    for year in tqdm(years):
        for rank in ranks:
            try:
                df_TIMES = pd.concat([df_TIMES,fetch_TIMES(rank=rank, year=year)], axis=0, ignore_index=True)
            except:
                print(year,rank)
    df_TIMES['Schema'] = 'TIMES'

    return df_TIMES

years = [2021]
ranks = ['World.University.Rankings']
df_TIMES = TIMES_rank(years, ranks)
print('\n === Times Higher Education ===')
display(df_TIMES.head(5))
```

    100%|██████████| 1/1 [00:01<00:00,  1.37s/it]


    
     === Times Higher Education ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>University</th>
      <th>TotalScore</th>
      <th>Teaching</th>
      <th>Research</th>
      <th>Citation</th>
      <th>Industry Income</th>
      <th>International Outlook</th>
      <th>Country</th>
      <th>Student Count</th>
      <th>Faculty/Student</th>
      <th>International Student%</th>
      <th>Female/Male</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>University of Oxford</td>
      <td>95.6</td>
      <td>91.300003</td>
      <td>99.599998</td>
      <td>98.000000</td>
      <td>68.699997</td>
      <td>96.400002</td>
      <td>United Kingdom</td>
      <td>20,774</td>
      <td>11.1</td>
      <td>41%</td>
      <td>46 : 54</td>
      <td>95.617500</td>
      <td>1.0</td>
      <td>World University Rankings</td>
      <td>1.0</td>
      <td>True</td>
      <td>2021</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Stanford University</td>
      <td>94.9</td>
      <td>92.199997</td>
      <td>96.699997</td>
      <td>99.900002</td>
      <td>90.099998</td>
      <td>79.500000</td>
      <td>United States</td>
      <td>16,223</td>
      <td>7.4</td>
      <td>23%</td>
      <td>44 : 56</td>
      <td>94.854999</td>
      <td>2.0</td>
      <td>World University Rankings</td>
      <td>1.0</td>
      <td>True</td>
      <td>2021</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Harvard University</td>
      <td>94.8</td>
      <td>94.400002</td>
      <td>98.800003</td>
      <td>99.400002</td>
      <td>46.799999</td>
      <td>77.699997</td>
      <td>United States</td>
      <td>21,261</td>
      <td>9.3</td>
      <td>25%</td>
      <td>49 : 51</td>
      <td>94.777502</td>
      <td>3.0</td>
      <td>World University Rankings</td>
      <td>2.0</td>
      <td>True</td>
      <td>2021</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>California Institute of Technology</td>
      <td>94.5</td>
      <td>92.500000</td>
      <td>96.900002</td>
      <td>97.000000</td>
      <td>92.699997</td>
      <td>83.599998</td>
      <td>United States</td>
      <td>2,238</td>
      <td>6.3</td>
      <td>33%</td>
      <td>36 : 64</td>
      <td>94.507500</td>
      <td>4.0</td>
      <td>World University Rankings</td>
      <td>3.0</td>
      <td>True</td>
      <td>2021</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Massachusetts Institute of Technology</td>
      <td>94.4</td>
      <td>90.699997</td>
      <td>94.400002</td>
      <td>99.699997</td>
      <td>90.400002</td>
      <td>90.000000</td>
      <td>United States</td>
      <td>11,276</td>
      <td>8.4</td>
      <td>34%</td>
      <td>39 : 61</td>
      <td>94.449999</td>
      <td>5.0</td>
      <td>World University Rankings</td>
      <td>4.0</td>
      <td>True</td>
      <td>2021</td>
      <td>TIMES</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === Times Higher Education Law ===')

years = [2020]
ranks = ['Subject.Law']
df_TIMES = TIMES_rank(years, ranks)
display(df_TIMES.head(5))

```

    100%|██████████| 1/1 [00:00<00:00,  2.41it/s]


    
     === Times Higher Education Law ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>University</th>
      <th>TotalScore</th>
      <th>Teaching</th>
      <th>Research</th>
      <th>Citation</th>
      <th>Industry Income</th>
      <th>International Outlook</th>
      <th>Country</th>
      <th>Student Count</th>
      <th>Faculty/Student</th>
      <th>International Student%</th>
      <th>Female/Male</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Stanford University</td>
      <td>82.3</td>
      <td>96.500000</td>
      <td>88.900002</td>
      <td>73.400002</td>
      <td>70.699997</td>
      <td>36.099998</td>
      <td>United States</td>
      <td>16,135</td>
      <td>7.3</td>
      <td>23%</td>
      <td>43 : 57</td>
      <td>82.303201</td>
      <td>1.0</td>
      <td>Law</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>University of Cambridge</td>
      <td>81.0</td>
      <td>82.199997</td>
      <td>91.000000</td>
      <td>67.300003</td>
      <td>37.099998</td>
      <td>92.800003</td>
      <td>United Kingdom</td>
      <td>18,978</td>
      <td>10.9</td>
      <td>37%</td>
      <td>47 : 53</td>
      <td>81.011900</td>
      <td>2.0</td>
      <td>Law</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Yale University</td>
      <td>79.3</td>
      <td>96.699997</td>
      <td>85.000000</td>
      <td>73.599998</td>
      <td>36.900002</td>
      <td>24.100000</td>
      <td>United States</td>
      <td>12,402</td>
      <td>5.4</td>
      <td>20%</td>
      <td>50 : 50</td>
      <td>79.292399</td>
      <td>3.0</td>
      <td>Law</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>University of Oxford</td>
      <td>78.3</td>
      <td>81.699997</td>
      <td>89.599998</td>
      <td>60.900002</td>
      <td>38.900002</td>
      <td>86.900002</td>
      <td>United Kingdom</td>
      <td>20,664</td>
      <td>11.2</td>
      <td>41%</td>
      <td>46 : 54</td>
      <td>78.331199</td>
      <td>4.0</td>
      <td>Law</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>TIMES</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>University of Chicago</td>
      <td>78.2</td>
      <td>96.000000</td>
      <td>87.699997</td>
      <td>64.400002</td>
      <td>37.099998</td>
      <td>30.799999</td>
      <td>United States</td>
      <td>13,833</td>
      <td>5.7</td>
      <td>28%</td>
      <td>46 : 54</td>
      <td>78.203099</td>
      <td>5.0</td>
      <td>Law</td>
      <td>3.0</td>
      <td>True</td>
      <td>2020</td>
      <td>TIMES</td>
    </tr>
  </tbody>
</table>
</div>


## ARWU World University Rankings
We extract [ARWU](http://www.shanghairanking.com) or the Shanghai Ranking via the table tag, as all required data are available these tags.
The tricky part would be to apply the weightings to each subject and adjustment to non-comprehensive university such as LSE.
Please refer to the [methodology](http://www.shanghairanking.com/ARWU-Methodology-2020.html).


```python
#Define ARWU subject and worling rank scraping function
def fetch_ARWU_subject(ARWU_subject, subject= "Mathematics", year = "current"):
    """Scrape ARWU Subject Page
    """
    if (year == "current"):
        url1 = "http://www.shanghairanking.com/Shanghairanking-Subject-Rankings/"
    else:
        url1 = "http://www.shanghairanking.com/Shanghairanking-Subject"+ "-Rankings-"+ str(year)+"/"
    subject_page = ARWU_subject[ARWU_subject.Subject==subject].Page.reset_index(drop=True)[0]
    url_subject = url1+subject_page
    r = requests.get(url_subject)
    soup = BeautifulSoup(r.content, "html.parser")
    table = soup.find(lambda tag: tag.name == 'table' and tag.has_attr('id') and tag['id'] == "UniversityRanking")
    list_table = tableDataText(table)
    df = pd.DataFrame(list_table[1:])
    if  year == "current":
        df = df.drop(columns = 3)
    df.columns = ["Rank", "University", "Country", "TotalScore", "PUB",
                        "CNCI", "IC", "TOP", "AWARD"]
    # Retrieve countries
    countries = soup.find(lambda tag: tag.name == 'table' and tag.has_attr('id') and tag['id'] == "UniversityRanking")
    countries = [td['title'] for td in countries.find_all('img')]
    df.Country = countries

    weightings = pd.read_csv('arwuweighting.csv')
    weightings = weightings[weightings.Ranktype==subject].reset_index(drop=True)
    df = df.replace('NA', 0, regex=True)
    df[["PUB", "CNCI", "IC", "TOP", "AWARD"]] =  df[["PUB","CNCI", "IC", "TOP", "AWARD"]].astype('float32')
    df['Calculated Score'] = np.sum(np.multiply(df[["PUB","CNCI", "IC", "TOP", "AWARD"]],
                             weightings[["PUB",  "Normalized Citation",  "IC",  "Number Top10",  "Award"]]/100),1)

    df['Calculated Rank'] = df['Calculated Score'].rank(method ='min',ascending = False)
    df['Subject'] = subject
    df['National Rank'] = df.groupby('Country')['Calculated Score'].rank(method ='min',ascending = False)
    df['Top 100'] = df['Calculated Rank'] <= 100
    if year == "current":
        df['Year'] = datetime.now().date().year
    else:
        df['Year'] = year
    return df

def fetch_ARWU(year = None):
    """Scrape ARWU World University Ranking Page
    """
    url1 = "http://www.shanghairanking.com/ARWU"+ str(year) + ".html"

    r = requests.get(url1)
    soup = BeautifulSoup(r.content, "html.parser")
    table = soup.find(lambda tag: tag.name == 'table' and tag.has_attr('id') and tag['id'] == "UniversityRanking")
    list_table = tableDataText(table)
    df = pd.DataFrame(list_table[1:])
    df.columns = ["Rank", "University", "Country", "National Rank",
		"TotalScore", "Alumni", "Award", "HiCi", "N&S", "PUB",
		"PCP"]
    # Retrieve countries
    countries = soup.find(lambda tag: tag.name == 'table' and tag.has_attr('id') and tag['id'] == "UniversityRanking")
    countries = [td['src'] for td in countries.find_all('img')]
    df.Country = countries
    df.Country  = df.Country.str.replace('image/flag/','')
    df.Country  = df.Country.str.replace('.png','')


    df = df.replace('NA', 0, regex=True)
    df = df.replace('', -0.01, regex=True)
    df[[ "Alumni", "Award", "HiCi", "N&S", "PUB","PCP"]] =  df[[ "Alumni", "Award", "HiCi", "N&S", "PUB","PCP"]].astype('float32')

    df['Calculated Score'] = 1
    df['Calculated Score'][df["N&S"] == -0.01] = np.sum(np.multiply(df[df["N&S"] == -0.01][["Alumni", "Award", "HiCi", "PUB","PCP"]],[0.1, 0.2, 0.2, 0.2, 0.1]),1)*1.25
    df['Calculated Score'][df["N&S"] != -0.01] = np.sum(np.multiply(df[df["N&S"] != -0.01][["Alumni", "Award", "HiCi","N&S", "PUB","PCP"]],[0.1, 0.2, 0.2, 0.2,0.2, 0.1]),1)
    df['Calculated Score'] = df['Calculated Score'] * 100/np.max(df['Calculated Score'])

    df['Calculated Rank'] = df['Calculated Score'].rank(method ='min',ascending = False)
    df['Subject'] = 'World'
    df['National Rank'] = df.groupby('Country')['Calculated Score'].rank(method ='min',ascending = False)
    df['Top 100'] = df['Calculated Rank'] <= 100
    df['Year'] = year

    return df

def ARWU_rank(years=[2020], first_x_subjects = 2):
   '''first_x_subjects: get results for the first n subjects in ARWU subject list'''
   df_ARWU =  pd.DataFrame()
   for year in tqdm(years):
       try:
           df_ARWU = df_ARWU.append(fetch_ARWU(year = year))
       except:
           pass

   df_ARWU['Schema'] = 'ARWU'

   ARWU_subject =  weightings['subject_arwu']
   df_ARWU_subject = pd.DataFrame()
   for year in years:
       if year == datetime.now().year:
           year = "current"
       for subject in tqdm(ARWU_subject.Subject[0:first_x_subjects]):
           try:
               df_ARWU_subject = df_ARWU_subject.append(fetch_ARWU_subject(ARWU_subject, subject= subject, year = year))
           except:
               pass

   df_ARWU_subject['Schema'] = 'ARWU'
   df_ARWU_subject.columns = ['Rank', 'University', 'Country', 'TotalScore', 'PUB', 'CNCI', 'IC',
           'TOP', 'Award', 'Calculated Score', 'Calculated Rank', 'Subject',
           'National Rank', 'Top 100', 'Year', 'Schema']


   return df_ARWU, df_ARWU_subject
```


```python
df_ARWU, df_ARWU_subject = ARWU_rank(years=[2020])

print('\n === ARWU ===')
display(df_ARWU.head(5))
```

      0%|          | 0/1 [00:00<?, ?it/s]/Users/jiezhu/.virtualenvs/globalenv/lib/python3.7/site-packages/ipykernel_launcher.py:68: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
    100%|██████████| 1/1 [00:04<00:00,  4.88s/it]
    100%|██████████| 2/2 [00:10<00:00,  5.26s/it]



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>University</th>
      <th>Country</th>
      <th>National Rank</th>
      <th>TotalScore</th>
      <th>Alumni</th>
      <th>Award</th>
      <th>HiCi</th>
      <th>N&amp;S</th>
      <th>PUB</th>
      <th>PCP</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Harvard University</td>
      <td>USA</td>
      <td>1.0</td>
      <td>100.0</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>79.300003</td>
      <td>100.000000</td>
      <td>1.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Stanford University</td>
      <td>USA</td>
      <td>2.0</td>
      <td>74.2</td>
      <td>43.799999</td>
      <td>86.599998</td>
      <td>71.099998</td>
      <td>79.500000</td>
      <td>77.099998</td>
      <td>53.799999</td>
      <td>74.155007</td>
      <td>2.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>University of Cambridge</td>
      <td>UK</td>
      <td>1.0</td>
      <td>70.6</td>
      <td>79.500000</td>
      <td>98.199997</td>
      <td>50.000000</td>
      <td>57.099998</td>
      <td>72.000000</td>
      <td>57.500000</td>
      <td>70.621872</td>
      <td>3.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Massachusetts Institute of Technology (MIT)</td>
      <td>USA</td>
      <td>3.0</td>
      <td>69.6</td>
      <td>71.400002</td>
      <td>85.099998</td>
      <td>51.400002</td>
      <td>69.800003</td>
      <td>63.700001</td>
      <td>69.699997</td>
      <td>69.549679</td>
      <td>4.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>University of California, Berkeley</td>
      <td>USA</td>
      <td>4.0</td>
      <td>65.8</td>
      <td>64.900002</td>
      <td>76.699997</td>
      <td>53.299999</td>
      <td>68.500000</td>
      <td>63.400002</td>
      <td>56.000000</td>
      <td>65.832737</td>
      <td>5.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Princeton University</td>
      <td>USA</td>
      <td>5.0</td>
      <td>61.1</td>
      <td>59.000000</td>
      <td>97.900002</td>
      <td>41.400002</td>
      <td>49.900002</td>
      <td>44.700001</td>
      <td>71.800003</td>
      <td>61.125295</td>
      <td>6.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Columbia University</td>
      <td>USA</td>
      <td>6.0</td>
      <td>58.6</td>
      <td>59.500000</td>
      <td>65.800003</td>
      <td>48.000000</td>
      <td>54.799999</td>
      <td>72.300003</td>
      <td>32.900002</td>
      <td>58.633719</td>
      <td>7.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>California Institute of Technology</td>
      <td>USA</td>
      <td>7.0</td>
      <td>57.7</td>
      <td>50.700001</td>
      <td>69.099998</td>
      <td>36.400002</td>
      <td>57.900002</td>
      <td>43.900002</td>
      <td>100.000000</td>
      <td>57.724906</td>
      <td>8.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>University of Oxford</td>
      <td>UK</td>
      <td>2.0</td>
      <td>57.2</td>
      <td>48.900002</td>
      <td>54.299999</td>
      <td>46.400002</td>
      <td>53.900002</td>
      <td>78.900002</td>
      <td>43.700001</td>
      <td>57.142858</td>
      <td>9.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>University of Chicago</td>
      <td>USA</td>
      <td>8.0</td>
      <td>54.6</td>
      <td>58.700001</td>
      <td>88.199997</td>
      <td>35.700001</td>
      <td>41.299999</td>
      <td>51.599998</td>
      <td>43.000000</td>
      <td>54.661492</td>
      <td>10.0</td>
      <td>World</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
  </tbody>
</table>
</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>University</th>
      <th>Country</th>
      <th>TotalScore</th>
      <th>PUB</th>
      <th>CNCI</th>
      <th>IC</th>
      <th>TOP</th>
      <th>Award</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Paris-Saclay University</td>
      <td>France</td>
      <td>362.9</td>
      <td>87.000000</td>
      <td>73.599998</td>
      <td>72.699997</td>
      <td>87.800003</td>
      <td>100.000000</td>
      <td>362.940001</td>
      <td>1.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Princeton University</td>
      <td>United States</td>
      <td>354.3</td>
      <td>71.400002</td>
      <td>88.900002</td>
      <td>64.400002</td>
      <td>100.000000</td>
      <td>81.199997</td>
      <td>354.380000</td>
      <td>2.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Sorbonne University</td>
      <td>France</td>
      <td>308.3</td>
      <td>100.000000</td>
      <td>72.000000</td>
      <td>72.599998</td>
      <td>95.599998</td>
      <td>26.100000</td>
      <td>308.219999</td>
      <td>3.0</td>
      <td>Mathematics</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Stanford University</td>
      <td>United States</td>
      <td>301.6</td>
      <td>66.099998</td>
      <td>90.800003</td>
      <td>63.299999</td>
      <td>89.400002</td>
      <td>42.599998</td>
      <td>301.560001</td>
      <td>4.0</td>
      <td>Mathematics</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>University of Cambridge</td>
      <td>United Kingdom</td>
      <td>301.4</td>
      <td>63.200001</td>
      <td>88.800003</td>
      <td>77.099998</td>
      <td>73.699997</td>
      <td>60.299999</td>
      <td>301.420000</td>
      <td>5.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Massachusetts Institute of Technology (MIT)</td>
      <td>United States</td>
      <td>293.5</td>
      <td>80.000000</td>
      <td>85.199997</td>
      <td>64.000000</td>
      <td>89.400002</td>
      <td>26.100000</td>
      <td>293.499999</td>
      <td>6.0</td>
      <td>Mathematics</td>
      <td>3.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>University of Oxford</td>
      <td>United Kingdom</td>
      <td>292.3</td>
      <td>78.199997</td>
      <td>75.599998</td>
      <td>76.000000</td>
      <td>75.599998</td>
      <td>47.700001</td>
      <td>292.299995</td>
      <td>7.0</td>
      <td>Mathematics</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>New York University</td>
      <td>United States</td>
      <td>288.4</td>
      <td>62.000000</td>
      <td>94.000000</td>
      <td>68.199997</td>
      <td>58.599998</td>
      <td>60.299999</td>
      <td>288.539997</td>
      <td>8.0</td>
      <td>Mathematics</td>
      <td>4.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>ETH Zurich</td>
      <td>Switzerland</td>
      <td>271.9</td>
      <td>71.300003</td>
      <td>78.400002</td>
      <td>81.300003</td>
      <td>63.200001</td>
      <td>42.599998</td>
      <td>271.760004</td>
      <td>9.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>PSL University</td>
      <td>France</td>
      <td>269.8</td>
      <td>72.199997</td>
      <td>83.199997</td>
      <td>72.800003</td>
      <td>69.699997</td>
      <td>30.200001</td>
      <td>269.859992</td>
      <td>10.0</td>
      <td>Mathematics</td>
      <td>3.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
  </tbody>
</table>
</div>



```python
print('\n === ARWU Subject Rankings ===')

display(df_ARWU_subject.head(5))

```

    
     === ARWU Subject Rankings ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>University</th>
      <th>Country</th>
      <th>TotalScore</th>
      <th>PUB</th>
      <th>CNCI</th>
      <th>IC</th>
      <th>TOP</th>
      <th>Award</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Paris-Saclay University</td>
      <td>France</td>
      <td>362.9</td>
      <td>87.000000</td>
      <td>73.599998</td>
      <td>72.699997</td>
      <td>87.800003</td>
      <td>100.000000</td>
      <td>362.940001</td>
      <td>1.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Princeton University</td>
      <td>United States</td>
      <td>354.3</td>
      <td>71.400002</td>
      <td>88.900002</td>
      <td>64.400002</td>
      <td>100.000000</td>
      <td>81.199997</td>
      <td>354.380000</td>
      <td>2.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Sorbonne University</td>
      <td>France</td>
      <td>308.3</td>
      <td>100.000000</td>
      <td>72.000000</td>
      <td>72.599998</td>
      <td>95.599998</td>
      <td>26.100000</td>
      <td>308.219999</td>
      <td>3.0</td>
      <td>Mathematics</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Stanford University</td>
      <td>United States</td>
      <td>301.6</td>
      <td>66.099998</td>
      <td>90.800003</td>
      <td>63.299999</td>
      <td>89.400002</td>
      <td>42.599998</td>
      <td>301.560001</td>
      <td>4.0</td>
      <td>Mathematics</td>
      <td>2.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>University of Cambridge</td>
      <td>United Kingdom</td>
      <td>301.4</td>
      <td>63.200001</td>
      <td>88.800003</td>
      <td>77.099998</td>
      <td>73.699997</td>
      <td>60.299999</td>
      <td>301.420000</td>
      <td>5.0</td>
      <td>Mathematics</td>
      <td>1.0</td>
      <td>True</td>
      <td>2020</td>
      <td>ARWU</td>
    </tr>
  </tbody>
</table>
</div>


## QS World University Rankings
[QS](https://www.topuniversities.com) adopted a similar as the Times Higher Education. We therefore use ajax based extraction to
extract data for both world and subject rankings. The weightings for the calculated rank are extracted from
[QS intelligence unit](http://www.iu.qs.com).


```python
#Define QS subject and world rank scraping function

def fetch_QS(rank= None, year = None, weightings = weightings['weightings_qs']):
    """Scrape QS Subject Page
    """
    with requests.Session() as session:
        if "world" in rank:
            url = "https://www.topuniversities.com/university-rankings/world-university-rankings/"+ str(year)
        else:
            url = "https://www.topuniversities.com/university-rankings/university-subject-rankings/"+ str(year) +"/"+ rank

        session.get(url)
        r = session.post(url,headers={"Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
                                  'X-Requested-With': 'XMLHttpRequest'})
        soup = BeautifulSoup(r.content, "lxml")
        scripts = soup.find_all('script')
        for script in scripts:
            try:
                if "jQuery.extend" in script.contents[0] :
                    jsonStr = script.contents[0].split('jQuery.extend(Drupal.settings,')[1]
                    jsonStr = jsonStr.rsplit(');', 1)[0]
                    jsonObj = json.loads(jsonStr)
                    url2 = jsonObj['qs_rankings_datatables']['rank_indicators_url']
            except:
                pass

    req2 = urllib.request.Request(url2, headers={'User-Agent': 'Mozilla/5.0'})
    with urllib.request.urlopen(req2) as url:
        indicator_data = json.loads(url.read().decode())

    columns  = pd.DataFrame(indicator_data['columns'])
    rank_data =  pd.DataFrame(indicator_data['data'])

    for index,row in rank_data.iterrows():
        rank_data.iloc[index] = [strip_tags(item) for item in row]
    if "world" in rank:
        rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
           'TotalScore', 'stars', 'Academic', '3791742_rank_d', '3791742_rank',
           'Employer', '3791741_rank_d', '3791741_rank', 'Faculty Student',
           '3791740_rank_d', '3791740_rank', 'Citation', '3791737_rank_d',
           '3791737_rank', 'International Faculty', '3791739_rank_d', '3791739_rank', 'International Student',
           '3791738_rank_d', '3791738_rank', '', '_rank_d', '_rank']
        rank_data = rank_data[['Country', 'Rank',  'University', 'TotalScore',  'Academic',  'Employer','Faculty Student',
        'Citation', 'International Faculty', 'International Student']]
    else:
        try:
            rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
                                 'TotalScore', 'stars', 'Academic', '4280115_rank_d', '4280115_rank',
                                 'Employer', '4280112_rank_d', '4280112_rank', 'h-index',
                                 '4280113_rank_d', '4280113_rank', 'Citation', '4280114_rank_d',
                                 '4280114_rank']
        except:
            if rank == 'performing-arts':
                rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
                                     'TotalScore', 'stars', 'Academic', '4280115_rank_d', '4280115_rank',
                                     'Employer', '4280112_rank_d', '4280112_rank']
                rank_data['h-index'] = 0
                rank_data['Citation'] = 0
            elif rank == 'classics-ancient-history':
                rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
                                     'TotalScore', 'stars', 'Academic', '4280115_rank_d', '4280115_rank',
                                     'Employer', '4280112_rank_d', '4280112_rank']
                rank_data['h-index'] = 0
                rank_data['Citation'] = 0
            elif rank == 'english-language-literature':
                rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
                                     'TotalScore', 'stars', 'Academic', '4280115_rank_d', '4280115_rank',
                                     'Employer', '4280112_rank_d', '4280112_rank', 'Citation', '4280114_rank_d',
                                     '4280114_rank']
                rank_data['h-index'] = 0
            elif rank == 'hospitality':
                rank_data.columns = ['region', 'Country', 'Rank', 'overall_rank_dis', 'University',
                                     'TotalScore', 'stars', 'Academic', '4280115_rank_d', '4280115_rank',
                                     'Employer', '4280112_rank_d', '4280112_rank', 'Citation', '4280114_rank_d',
                                     '4280114_rank']
                rank_data['h-index'] = 0
            else:
                pass

        rank_data = rank_data[['Country', 'Rank', 'University', 'TotalScore', 'Academic', 'Employer', 'h-index', 'Citation']]

    weightings.Subject = weightings.Subject.str.lower()
    weightings.Subject = weightings.Subject.str.replace('.','-')
    weightings = weightings[weightings.Subject==rank].reset_index(drop=True)
    df = rank_data.copy()

    df = df.replace('', 0, regex=True)

    if "world" in rank:
        df[[ 'Academic',  'Employer','Faculty Student',
        'Citation', 'International Faculty', 'International Student']] = \
            df[[ 'Academic',  'Employer','Faculty Student',
        'Citation', 'International Faculty', 'International Student']].astype('float32')

        df['Calculated Score'] = np.sum(np.multiply(df[['Academic',  'Employer','Faculty Student', 'Citation', 'International Faculty', 'International Student']],
                                 weightings[['Academic',  'Employer','Faculty Student', 'Citation', 'International Faculty', 'International Student']]),1)
        df['Calculated Score'] = 100 / np.max(df['Calculated Score']) * df['Calculated Score']
    else:
        df[['Academic', 'Employer', 'h-index', 'Citation']] =  df[['Academic', 'Employer', 'h-index', 'Citation']].astype('float32')
        df['Calculated Score'] = np.sum(np.multiply(df[['Academic', 'Employer', 'h-index', 'Citation']],
                                                    weightings[['Academic', 'Employer', 'h-index', 'Citation']]), 1)


    df['Calculated Rank'] = df['Calculated Score'].rank(method ='min',ascending = False)
    df['Subject'] =  rank.replace('.',' ')

    df['National Rank'] = df.groupby('Country')['Calculated Score'].rank(method ='min',ascending = False)
    df['Top 100'] = df['Calculated Rank'] <= 100
    df['Year'] = year-1

    return df

def QS_rank(years=None, ranks=None):

    df_QS = pd.DataFrame()
    for year in tqdm(years):
        for rank in ranks:
            try:
                df_QS = df_QS.append(fetch_QS(rank=rank, year=year))
            except:
                print(year, rank)
    df_QS['Schema'] = 'QS'
    return df_QS
```


```python
years = [2020]
df_QS = QS_rank(years = years, ranks = ranks)
ranks=['world-university-rankings','classics-ancient-history']

```

    100%|██████████| 1/1 [00:10<00:00, 10.13s/it]



```python
print('\n === QS World and Subject Rankings ===')
display(df_QS[df_QS.Subject== 'world-university-rankings'].head(5))

display(df_QS[df_QS.Subject== 'classics-ancient-history'].head(5))



```

    
     === QS World and Subject Rankings ===



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Rank</th>
      <th>University</th>
      <th>TotalScore</th>
      <th>Academic</th>
      <th>Employer</th>
      <th>Faculty Student</th>
      <th>Citation</th>
      <th>International Faculty</th>
      <th>International Student</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>h-index</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United States</td>
      <td>1</td>
      <td>Massachusetts Institute of Technology (MIT)</td>
      <td>100</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>99.800003</td>
      <td>100.000000</td>
      <td>94.099998</td>
      <td>100.000000</td>
      <td>1.0</td>
      <td>world-university-rankings</td>
      <td>1.0</td>
      <td>True</td>
      <td>2019</td>
      <td>NaN</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>United States</td>
      <td>2</td>
      <td>Stanford University</td>
      <td>98.4</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>98.599998</td>
      <td>99.800003</td>
      <td>67.699997</td>
      <td>98.424722</td>
      <td>2.0</td>
      <td>world-university-rankings</td>
      <td>2.0</td>
      <td>True</td>
      <td>2019</td>
      <td>NaN</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>United States</td>
      <td>3</td>
      <td>Harvard University</td>
      <td>97.4</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>98.699997</td>
      <td>99.599998</td>
      <td>86.300003</td>
      <td>62.200001</td>
      <td>97.411327</td>
      <td>3.0</td>
      <td>world-university-rankings</td>
      <td>3.0</td>
      <td>True</td>
      <td>2019</td>
      <td>NaN</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>3</th>
      <td>United Kingdom</td>
      <td>4</td>
      <td>University of Oxford</td>
      <td>97.2</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>84.699997</td>
      <td>99.699997</td>
      <td>98.500000</td>
      <td>97.175537</td>
      <td>4.0</td>
      <td>world-university-rankings</td>
      <td>1.0</td>
      <td>True</td>
      <td>2019</td>
      <td>NaN</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United States</td>
      <td>5</td>
      <td>California Institute of Technology (Caltech)</td>
      <td>96.9</td>
      <td>97.800003</td>
      <td>81.199997</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>99.400002</td>
      <td>87.300003</td>
      <td>96.899614</td>
      <td>5.0</td>
      <td>world-university-rankings</td>
      <td>4.0</td>
      <td>True</td>
      <td>2019</td>
      <td>NaN</td>
      <td>QS</td>
    </tr>
  </tbody>
</table>
</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Rank</th>
      <th>University</th>
      <th>TotalScore</th>
      <th>Academic</th>
      <th>Employer</th>
      <th>Faculty Student</th>
      <th>Citation</th>
      <th>International Faculty</th>
      <th>International Student</th>
      <th>Calculated Score</th>
      <th>Calculated Rank</th>
      <th>Subject</th>
      <th>National Rank</th>
      <th>Top 100</th>
      <th>Year</th>
      <th>h-index</th>
      <th>Schema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United Kingdom</td>
      <td>1</td>
      <td>University of Oxford</td>
      <td>97.7</td>
      <td>97.599998</td>
      <td>98.699997</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97.709998</td>
      <td>1.0</td>
      <td>classics-ancient-history</td>
      <td>1.0</td>
      <td>True</td>
      <td>2019</td>
      <td>0.0</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Italy</td>
      <td>2</td>
      <td>Sapienza University of Rome</td>
      <td>97</td>
      <td>99.599998</td>
      <td>73.300003</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>96.969999</td>
      <td>2.0</td>
      <td>classics-ancient-history</td>
      <td>1.0</td>
      <td>True</td>
      <td>2019</td>
      <td>0.0</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>United Kingdom</td>
      <td>3</td>
      <td>University of Cambridge</td>
      <td>96.9</td>
      <td>96.699997</td>
      <td>98.400002</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>96.869997</td>
      <td>3.0</td>
      <td>classics-ancient-history</td>
      <td>2.0</td>
      <td>True</td>
      <td>2019</td>
      <td>0.0</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Germany</td>
      <td>4</td>
      <td>Ruprecht-Karls-Universität Heidelberg</td>
      <td>96</td>
      <td>100.000000</td>
      <td>60.200001</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>96.020000</td>
      <td>4.0</td>
      <td>classics-ancient-history</td>
      <td>1.0</td>
      <td>True</td>
      <td>2019</td>
      <td>0.0</td>
      <td>QS</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Germany</td>
      <td>5</td>
      <td>Ludwig-Maximilians-Universität München</td>
      <td>95</td>
      <td>98.500000</td>
      <td>63.299999</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>94.980000</td>
      <td>5.0</td>
      <td>classics-ancient-history</td>
      <td>2.0</td>
      <td>True</td>
      <td>2019</td>
      <td>0.0</td>
      <td>QS</td>
    </tr>
  </tbody>
</table>
</div>

