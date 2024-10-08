<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]




<!-- PROJECT LOGO -->
<br />
<h3 align="center">Dave3625 - Lab1</h3>
<p align="center">
  <a href="https://github.com/DAVE3625/DAVE3625-24H/tree/main/Lab1">
    <img src="img/logo.png" alt="Data wrangling" width="auto" height="auto">
  </a>

  

  <p align="center">
    An exercise in pandas for cleaning and plotting a dataset <br \>
    <br />
    ·
    <a href="https://github.com/DAVE3625/DAVE3625-24H/issues">Report Bug</a>
    ·
    <a href="https://github.com/DAVE3625/DAVE3625-24H/issues">Request Feature</a>
  </p>
</p>


<!-- ABOUT THE LAB -->
## About The Lab
Most of the time spent working on AI is time spent preparing data. You need to figure out what data points to use, and if you can combine data points to get a better model. 

During this week's first lab, we will do a deep dive into [Pandas][Pandas] DataFrames and look at visualization libraries like Matplotlib, Seaborn, and Plotly.

We will be using [pandas][pandas-doc], [matplotlib][matplotlib-doc], [seaborn][seaborn-doc] and [numpy][numpy-doc].


----------------------------------------------

This week's second lab will involve going through the student dataset in the file stud.csv. 

That DataFrame has 50 entries with:
StudentID, Age, email, hrsStudy, FinalGrade


<details>
<summary>Tasks for thursdays lab</summary>

  ## Tasks
  
  **[Solution][Solution]**
  
  **1. In this lab, you will import the csv file into pandas:**
  
  Hint: 
  ```
  #If you want to use the csv from this git set
  # url = "https://github.com/DAVE3625/DAVE3625-24H/blob/main/Lab1/stud.csv"
  # You can also download the csv and set
  # url="{filepath]/stud.csv"
  df = pd.read_csv(url, sep=',')
  df.head()
  
  ```
  
  
  **2. You will then clean the data set so df.info() produce**
  
  ![dfinfo][dfinfo]
  
  Hint: 
  ```
  df.isna().sum() #show missing values
  df=df.replace(r'^\s*$', np.nan, regex=True) #Replace blank values with np.nan values
  
  df['Column'] = df['Column'].astype(str).astype(int) #Convert from obj to int
  ```
  **3. Then idenify and remove the outliers in the «FinalGrade» column**
  
  Hint : 
  ```
  df["FinalGrade"].plot.box()
  ```
  
  **4. Finally add a column “Grade” where you transform the grade from float to a char:**
  
  [Hint][columns-condition]
  ```
  91 - 100 = A
  81 - 90  = B
  71 - 80  = C
  61 – 70  = D
  51 – 60  = E
     > 50  = F
  ```
  **5. Produce this plot:**
  
  ![barplot]
  
  The dataset is generated with this script and errors added after it's creation:
  ```python
  import random
  print(StudentID,Age,email,hrsStudy,FinalGrade)
  for i in range(50):
     studId ="s" + str(random.randrange(10000,99999,1)) 
     print(str(studId)+","+ str(random.randrange(19,35,1))+",
        "+str(studId+"@oslomet.no"+","+str(random.randint(0, 12)))+","+str(random.randint(20, 100)))
  ```
  
  ## More hints
  
  Due to many questions about pandas and python in general i'll provide some extra hints
  
  **Q: I get an error when running**
  ```python
  df = pd.read_csv(url, sep=',')
  ```
  **A: This might be caused by two different problems**
  1.  Check your imports, for this lab you should consider these imports
  ```python
  #Import modules
  %matplotlib inline
  import pandas as pd
  import numpy as np
  from scipy import stats
  ```
  2.  If you have imported pandas, check that you assign a value to the variable **url**
  
  **Q: I can't convert values to int or float**
  Even after running
  ```python
  df=df.replace(r'^\s*$', np.nan, regex=True)
  ```
  **A: Running the above code only replace whitespace with a nan value**
  
  nan stands for Not a Number, and can not be converted to int or float. The reason we convert missing values to nan is that pandas lets us handle those values quite simple.
  If you want to assign nan's a value, you can use
  ```python
  df["Column"].replace(np.nan, VALUE, inplace=True)
  #Column is a placeholder for the column you want to change. 
  #In this example we have the columns StudentID,Age,email,hrsStudy,FinalGrade
  ```
  After you have replaced the nan values you want, you can drop rows containing nan with:
  ```python
  df.dropna(inplace = True)
  ```
  **Q: df["FinalGrade"].plot.box() don't work**
  
  1.  When running this code I get an error
  2.  The code run, but I can't see a plot
  
  **A:**
  
  1.  If you get an error and your code looks correct, try to reinstall matplotlib.
      Go to your conda prompt (make sure you're in the right env) and write:
      ```
      conda uninstall matplotlib
      conda update
      conda install matplotlib
      ```
      rest the kernel in jupyter notebook and try again
  
  2.  If your code runs, but only produce
  ```
  <matplotlib.axes._subplots.AxesSubplot at 0x7f7cb044f7d0>
  ```
  add 
  ```
  %matplotlib inline
  ````
  in the includes section
  
  **Q: How do I remove outliers?**
  
  **A:**
  Check [kite][kite-outliers] for a hint.
  On this set edit
  ```python
  filtered_entries = (abs_z_scores < 3).all(axis=1)
  #to
  filtered_entries = (abs_z_scores < 3)
  ```
  **Q: Can you provide some tutorials for jupyter and pandas?**
  
  I need some good tutorials to get me started. Can you recommend any?
  
  **A: Yes**
  
  If you are new to jupyter notebook and pandas [this youtube video][jupyter-tutorial] will be useful.
  
  [This site][pandas-tutorial] covers many important aspects of pandas, and I use it often as a reference.

</details>

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.






<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[issues-shield]: https://img.shields.io/github/issues/umaimehm/Intro_to_AI_2021.svg?style=for-the-badge
[issues-url]: https://github.com/DAVE3625/DAVE3625-24H/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/DAVE3625/DAVE3625-24H/blob/main/Lab1/LICENSE

[dfinfo]: img/dfinfo.png
[barplot]: img/barplot.png
[seaborn-doc]: https://seaborn.pydata.org/
[matplotlib-doc]: https://matplotlib.org/stable/index.html
[pandas-doc]: https://pandas.pydata.org/docs/reference/index.html#api
[numpy-doc]: https://numpy.org/doc/stable/
[columns-condition]: https://www.dataquest.io/blog/tutorial-add-column-pandas-dataframe-based-on-if-else-condition/
[kite-outliers]: https://www.kite.com/python/answers/how-to-remove-outliers-from-a-pandas-dataframe-in-python/
[pandas-tutorial]: https://github.com/TirendazAcademy/PANDAS-TUTORIAL
[jupyter-tutorial]: https://www.youtube.com/watch?v=vmEHCJofslg
[solution]: Solution.ipynb
[Pandas]: Pandas.ipynb
