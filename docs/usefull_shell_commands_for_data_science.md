---

**Foreword**

Code snippets and excerpts from the tutorial. bash. From DataCamp.

---

# Quick notes

Use bash or alternative such as zsh.

Examples are based on the [adult](http://archive.ics.uci.edu/ml/machine-learning-databases/adult/) dataset from the UCI Machine Learning repository (Census Income dataset). This data set is commonly used to predict whether income exceeds $50K/yr based on census data. With 48842 rows and 14 attributes.

Move to the directory with `cd <dir>` and print the current working directory with `pwd`. Move up with `cd ..`.

# Count with `wc`


```bash
# count lines
wc -l adult.data
```

    32562 adult.data



```bash
# count words
wc -w adult.data
```

    488415 adult.data



```bash
ls -l
```

    total 9540
    -rw-rw-r-- 1 ugo ugo 3974305 jan 17 19:47 adult.data
    drwxrwxr-x 2 ugo ugo    4096 jan 17 19:59 adult
    -rw-rw-r-- 1 ugo ugo 5776165 jan 19 14:37 os
    -rw-rw-r-- 1 ugo ugo    6619 jan 19 14:37 Usefull shell commands for Data Science.ipynb



```bash
ls -l folder
```

    total 0
    -rw-rw-r-- 1 ugo ugo 0 jan 17 19:57 Nouveau document 1
    -rw-rw-r-- 1 ugo ugo 0 jan 17 19:57 Nouveau document 2



```bash
# count files
ls -l folder | wc -l
```

    3



```bash
# print head (10 by default or -n)
head -n 2 adult.data
```

    39, State-gov, 77516, Bachelors, 13, Never-married, Adm-clerical, Not-in-family, White, Male, 2174, 0, 40, United-States, <=50K
    50, Self-emp-not-inc, 83311, Bachelors, 13, Married-civ-spouse, Exec-managerial, Husband, White, Male, 0, 0, 13, United-States, <=50K


# Concatenate with `cat`

- Print a file content with `cat adult.data`.
- Concatenate files and create (replace) a file with `>`. `>>` will appends.


```bash
cat adult.data adult.data > target_file.csv
```

Add the header to the original file.


```bash
echo "age,workclass,fnlwgt,education,education-num,marital-status,occupation,relationship,race,sex,capital-gain,capital-loss,native-country,class" > header.csv
```

Add the header and rename the file.


```bash
cat header.csv adult.data > adult.csv
```

Check the first and last row (the default is 10 lines unless specified otherwise).


```bash
head -n 1 adult.csv
```

    age,workclass,fnlwgt,education,education-num,marital-status,occupation,relationship,race,sex,capital-gain,capital-loss,native-country,class



```bash
tail -n 2 adult.csv
```

    52, Self-emp-inc, 287927, HS-grad, 9, Married-civ-spouse, Exec-managerial, Wife, White, Female, 15024, 0, 40, United-States, >50K
    


# Modify with `sed`

When a file is corrupted or badly formatted, with no UTF-8 characters or misplaced comma.

```bash
sed "s/<string to replace>/<string to replace it with>/g" <source_file> > <target_file>.
```

Replace `?` for missing value with `NaN`. 

First, count the instances.


```bash
grep ", ?," adult.csv | wc -l
```

    2399


Second, 

- replace all the columns with `?`...
    - `"s/<string to replace>/"`.
- by an empty string...
    - `"/<string to replace it with>/g"`. Use column delimiter `,`.


```bash
sed "s/, ?,/,,/g" adult.csv > adult_v2.csv
```

# Subset

Large file (30M rows and more). Sample the head or the tail.

Extract the head (120 lines).


```bash
head -n 120 adult_v2.csv > adult_v3.csv
```

Extract the tail (12 lines).


```bash
tail -n 12 adult_v2.csv > adult_v4.csv
```

Extract 20 lines starting at line 100.


```bash
head -n 120 adult_v2.csv | tail -n 20 > adult_sample.csv
```

Add the header to the file without.


```bash
cat header.csv adult_v4.csv > adult_v4_with_header.csv
```


```bash
cat header.csv adult_sample.csv > adult_sample_with_header.csv
```

# Find duplicates with `uniq`

Find adjacent repeated lines in a file.

- `uniq -c` adds the repetition count to each line.
- `uniq -d` only outputs duplicate lines.
- `uniq -u` only outputs unique lines.

First, sort the file to bunch duplicates together. Second, count the duplicates.


```bash
sort adult_v2.csv | uniq -d | wc -l
```

    23


Third, sort the file again, find the duplicates, sort the results in reverse, and output the first 3 duplicates. 


```bash
sort adult_v2.csv | uniq -c | sort -r | head -n 3
```

          3 25, Private, 195994, 1st-4th, 2, Never-married, Priv-house-serv, Not-in-family, White, Female, 0, 0, 40, Guatemala, <=50K
          2 90, Private, 52386, Some-college, 10, Never-married, Other-service, Not-in-family, Asian-Pac-Islander, Male, 0, 0, 35, United-States, <=50K
          2 49, Self-emp-not-inc, 43479, Some-college, 10, Married-civ-spouse, Craft-repair, Husband, White, Male, 0, 0, 40, United-States, <=50K


# Select columns with `cut`

Select a particular column. `-d` specifies the column delimiter and `-f` specifies the columns.

Find the number of unique values taken by the categorical variable `workclass` (2nd column of the file) and print the head of the results.


```bash
cut -d "," -f 2 adult_v2.csv | head -3
```

    workclass
     State-gov
     Self-emp-not-inc


Repeat, but this time, sort the results and find the duplicates.


```bash
cut -d "," -f 2 adult_v2.csv | sort | uniq -c
```

       1837 
        960  Federal-gov
       2093  Local-gov
          7  Never-worked
      22696  Private
       1116  Self-emp-inc
       2541  Self-emp-not-inc
       1298  State-gov
         14  Without-pay
          1 workclass


# Loop

Work of several files with loops.

Replace one character with another within all files inside a directory. Here is how to declare variables and call variables.


```bash
varname1=10
varname2='hello'
varname3=123.4
```


```bash
echo $varname1
```

    10



```bash
echo $varname2
```

    hello



```bash
echo $varname3
```

    123.4


First, declare two variables. Second, loop through the folder with `for`. Third, replace the character. Finally, for each file, create a new file.

```bash
replace_source=' '
replace_target='_'
for filename in ./*.csv; do
    new_filename=${filename//$replace_source/$replace_target}
    mv "$filename" "$new_filename"
done
```

With the `while` loop. However, `for` loops are faster.

```bash
replace_source=' '
replace_target='_'
while true; do
    new_filename=${filename//$replace_source/$replace_target}
    mv "$filename" "$new_filename"
done
```
