

```python
## Option 2: Academy of Py

# ![Education](Images/education.jpg)

# Well done! Having spent years analyzing financial records for big banks, you've finally scratched your idealistic itch and joined the education sector. In your latest role, you've become the Chief Data Scientist for your city's school district. In this capacity, you'll be helping the  school board and mayor make strategic decisions regarding future school budgets and priorities.

# As a first task, you've been asked to analyze the district-wide standardized test results. You'll be given access to every student's math and reading scores, as well as various information on the schools they attend. Your responsibility is to aggregate the data to and showcase obvious trends in school performance. 

# Your final report should include each of the following:

# **District Summary**

# * Create a high level snapshot (in table form) of the district's key metrics, including:
#   * Total Schools
#   * Total Students
#   * Total Budget
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

# **School Summary**

# * Create an overview table that summarizes key metrics about each school, including:
#   * School Name
#   * School Type
#   * Total Students
#   * Total School Budget
#   * Per Student Budget
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

# **Top Performing Schools (By Passing Rate)**

# * Create a table that highlights the top 5 performing schools based on Overall Passing Rate. Include:
#   * School Name
#   * School Type
#   * Total Students
#   * Total School Budget
#   * Per Student Budget
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

# **Top Performing Schools (By Passing Rate)**

# * Create a table that highlights the bottom 5 performing schools based on Overall Passing Rate. Include all of the same metrics as above.

# **Math Scores by Grade**

# * Create a table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.

# **Reading Scores by Grade**

# * Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.

# **Scores by School Spending**

# * Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

# **Scores by School Size**

# * Repeat the above breakdown, but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).

# **Scores by School Type**

# * Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).

# As final considerations:

# * Your script must work for both data-sets given.
# * You must use the Pandas Library and the Jupyter Notebook.
# * You must submit a link to your Jupyter Notebook with the viewable Data Frames. 
# * You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.  
# * You must include a written description of three observable trends based on the data. 
# * See [Example Solution](PyCitySchools/PyCitySchools_Example.pdf) for a reference on the expected format. 
```


```python
import os
import csv
import pandas as pd

school_path = os.path.join("raw_data", "schools_complete.csv") 
school_df = pd.read_csv(school_path)
stu_path = os.path.join("raw_data", "students_complete.csv") 
students_df = pd.read_csv(stu_path)


######Not Sure of passing rate so made a variable#########
passing_rate = 60

```


```python
students_df.head()
```




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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_df
```




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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
  </tbody>
</table>
</div>




```python
# * Create a high level snapshot (in table form) of the district's key metrics, including:
#   * Total Schools
#   * Total Students
#   * Total Budget
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

total_schools = len(school_df["name"])
total_students = len(students_df["name"])  #sum(school_df["size"])
total_budget = sum(school_df["budget"])
avg_math = students_df["math_score"].mean()
avg_reading = students_df["reading_score"].mean()
pct_math = (len(students_df[(students_df['math_score'] >= passing_rate)]) / total_students)

pct_reading = (len(students_df[(students_df['reading_score'] >= passing_rate)]) / total_students)
overall_passing = (pct_math + pct_reading) / 2
```


```python
# **District Summary**  FORMATTING 
district_summary = {

    "Total Schools": (total_schools),
    "Total Students": (total_students),
    "Total Budget": (total_budget),
    "Average Math Score": (avg_math),
    "Average Reading Score": (avg_reading),
    "% Passing Math": (pct_math),
    "% Passing Reading": (pct_reading),
    "Overall Passing Rate": (overall_passing)
    
}
ds_df = pd.DataFrame([district_summary], 
                     columns=["Total Schools","Total Students","Total Budget","Average Math Score","Average Reading Score","% Passing Math","% Passing Reading","Overall Passing Rate"])

ds_df.style.format({"% Passing Math": "{:.2%}", "% Passing Reading": "{:.2%}", "Overall Passing Rate": "{:.2%}", "Total Budget":"${:}" })



```




<style  type="text/css" >
</style>  
<table id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Schools</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total Budget</th> 
        <th class="col_heading level0 col3" >Average Math Score</th> 
        <th class="col_heading level0 col4" >Average Reading Score</th> 
        <th class="col_heading level0 col5" >% Passing Math</th> 
        <th class="col_heading level0 col6" >% Passing Reading</th> 
        <th class="col_heading level0 col7" >Overall Passing Rate</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160level0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col0" class="data row0 col0" >15</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col1" class="data row0 col1" >39170</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col2" class="data row0 col2" >$24649428</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col3" class="data row0 col3" >78.9854</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col4" class="data row0 col4" >81.8778</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col5" class="data row0 col5" >92.45%</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col6" class="data row0 col6" >100.00%</td> 
        <td id="T_e02f4dca_54c6_11e8_8bbe_4a0002456160row0_col7" class="data row0 col7" >96.22%</td> 
    </tr></tbody> 
</table> 




```python
# * Create an overview table that summarizes key metrics about each school, including:
#   * School Name
#   * School Type
#   * Total Students
#   * Total School Budget
#   * Per Student Budget
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

school_sum_df = school_df[["name", "type","size","budget"]]


school_sum_df["Per Student Budget"]=(school_sum_df["budget"] /school_sum_df["size"])

school_sum_df["Average Math Score"] = [students_df[(students_df['school'] == s_name)]['math_score'].mean() for s_name in school_sum_df["name"]]
school_sum_df["Average Reading Score"] = [students_df[(students_df['school'] == s_name)]['reading_score'].mean() for s_name in school_sum_df["name"]]

#####################################################
school_sum_df["% Passing Math"] = [len(
                        students_df[
                        (students_df['school'] == school_sum_df["name"][i]) & 
                        (students_df['math_score'] >= passing_rate)]) 
                        / school_sum_df['size'][i] 
                        for i in range(school_sum_df["name"].count())]

school_sum_df["% Passing Reading"] = [len(students_df[(students_df['school'] == school_sum_df["name"][i]) & (students_df['reading_score'] >= passing_rate)]) / school_sum_df['size'][i] for i in range(school_sum_df["name"].count())]
#
#    For i in range(# of schools) 
#        Flag all entries in student_df THAT
#           (students_df name matches school_sum_df name)  AND
#           (students_df score is above passing)
#      
#      divide length of flagged by size of that school  
#
#####################################################

school_sum_df["Overall Passing Rate"] = (school_sum_df["% Passing Reading"] + school_sum_df["% Passing Math"]) /2



```


```python
# **School Summary**  FORMATTING 
school_sum_df = school_sum_df.rename(columns = {"name":"Name","type":"School Type","size":"Total Students","budget":"Total School Budget"})
school_sum_df.set_index("Name", inplace=True)
school_sum_df

```




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.895297</td>
      <td>1.0</td>
      <td>0.947649</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.893027</td>
      <td>1.0</td>
      <td>0.946513</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# **Top Performing Schools (By Passing Rate)**

# * Create a table that highlights the top 5 performing schools based on Overall Passing Rate. Include:

school_sum_df.sort_values(by='Overall Passing Rate', ascending=False).head(5)
```




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# * Create a table that highlights the bottom 5 performing schools based on Overall Passing Rate. Include all of the same metrics as above.

school_sum_df.sort_values(by='Overall Passing Rate', ascending=True).head(5)
```




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
    </tr>
  </tbody>
</table>
</div>




```python
#groupedby School and Grade doesn't correctly outputs
grouped =  students_df.groupby(["school","grade"])
grouped["math_score"].mean()
```




    school                 grade
    Bailey High School     10th     76.996772
                           11th     77.515588
                           12th     76.492218
                           9th      77.083676
    Cabrera High School    10th     83.154506
                           11th     82.765560
                           12th     83.277487
                           9th      83.094697
    Figueroa High School   10th     76.539974
                           11th     76.884344
                           12th     77.151369
                           9th      76.403037
    Ford High School       10th     77.672316
                           11th     76.918058
                           12th     76.179963
                           9th      77.361345
    Griffin High School    10th     84.229064
                           11th     83.842105
                           12th     83.356164
                           9th      82.044010
    Hernandez High School  10th     77.337408
                           11th     77.136029
                           12th     77.186567
                           9th      77.438495
    Holden High School     10th     83.429825
                           11th     85.000000
                           12th     82.855422
                           9th      83.787402
    Huang High School      10th     75.908735
                           11th     76.446602
                           12th     77.225641
                           9th      77.027251
    Johnson High School    10th     76.691117
                           11th     77.491653
                           12th     76.863248
                           9th      77.187857
    Pena High School       10th     83.372000
                           11th     84.328125
                           12th     84.121547
                           9th      83.625455
    Rodriguez High School  10th     76.612500
                           11th     76.395626
                           12th     77.690748
                           9th      76.859966
    Shelton High School    10th     82.917411
                           11th     83.383495
                           12th     83.778976
                           9th      83.420755
    Thomas High School     10th     83.087886
                           11th     83.498795
                           12th     83.497041
                           9th      83.590022
    Wilson High School     10th     83.724422
                           11th     83.195326
                           12th     83.035794
                           9th      83.085578
    Wright High School     10th     84.010288
                           11th     83.836782
                           12th     83.644986
                           9th      83.264706
    Name: math_score, dtype: float64




```python
# **Math Scores by Grade**
# * Create a table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.


math_by_grade = school_df[["name"]]
math_by_grade["9th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '9th')]['math_score'].mean() for name in math_by_grade["name"]]
math_by_grade["10th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '10th')]['math_score'].mean() for name in math_by_grade["name"]]
math_by_grade["11th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '11th')]['math_score'].mean() for name in math_by_grade["name"]]
math_by_grade["12th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '12th')]['math_score'].mean() for name in math_by_grade["name"]]

#grabs each name from math_by_grade and uses it grab anything that matches school_name and grade
#then avg the math scores



math_by_grade.set_index('name')

```

    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys
    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      





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
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
  </tbody>
</table>
</div>




```python
# **Reading Scores by Grade**
# * Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.


reading_by_grade = school_df[["name"]]
reading_by_grade["9th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '9th')]['reading_score'].mean() for name in reading_by_grade["name"]]
reading_by_grade["10th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '10th')]['reading_score'].mean() for name in reading_by_grade["name"]]
reading_by_grade["11th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '11th')]['reading_score'].mean() for name in reading_by_grade["name"]]
reading_by_grade["12th"] = [students_df.loc[(students_df['school'] == name) & (students_df['grade'] == '12th')]['reading_score'].mean() for name in reading_by_grade["name"]]

reading_by_grade.set_index('name')
```

    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys
    /Users/stevenorn/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      





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
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
  </tbody>
</table>
</div>




```python
########### BINNING ##############
spending_bin = [0, 585, 615, 645, 675]
size_bin = [0, 1000, 2000, 5000]


spending_names = ['<$585', '$585-615', '$615-645', '$645-675']
size_names = ['Small(<1000)', 'Medium(1000-2000)', 'Larg(2000-5000)']

school_sum_bin = school_sum_df

school_sum_bin["School Spending"] = pd.cut(school_sum_bin["Per Student Budget"], spending_bin, labels=spending_names)
school_sum_bin["School Size"] = pd.cut(school_sum_bin["Total Students"], size_bin, labels=size_names)

```


```python
# **Scores by School Spending**

# * Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
#   * Average Math Score
#   * Average Reading Score
#   * % Passing Math
#   * % Passing Reading
#   * Overall Passing Rate (Average of the above two)

spending_bin = school_sum_bin.groupby('School Spending')
spending_bin["Average Math Score","Average Reading Score","% Passing Math", "% Passing Reading", "Overall Passing Rate"].mean()
```




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Spending</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>79.079225</td>
      <td>81.891436</td>
      <td>0.926361</td>
      <td>1.0</td>
      <td>0.963180</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>76.997210</td>
      <td>81.027843</td>
      <td>0.890415</td>
      <td>1.0</td>
      <td>0.945207</td>
    </tr>
  </tbody>
</table>
</div>




```python
# **Scores by School Size**

size_bin = school_sum_bin.groupby('School Size')
size_bin["Average Math Score","Average Reading Score","% Passing Math", "% Passing Reading", "Overall Passing Rate"].mean()
```




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small(&lt;1000)</th>
      <td>83.821598</td>
      <td>83.929843</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Medium(1000-2000)</th>
      <td>83.374684</td>
      <td>83.864438</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Larg(2000-5000)</th>
      <td>77.746417</td>
      <td>81.344493</td>
      <td>0.903676</td>
      <td>1.0</td>
      <td>0.951838</td>
    </tr>
  </tbody>
</table>
</div>




```python
# **Scores by School Type**

type_bin = school_sum_bin.groupby('School Type')
type_bin["Average Math Score","Average Reading Score","% Passing Math", "% Passing Reading", "Overall Passing Rate"].mean()
```




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>0.889915</td>
      <td>1.0</td>
      <td>0.944958</td>
    </tr>
  </tbody>
</table>
</div>


