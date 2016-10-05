# Hints for Exercise 5
Below are some tips for working on Exercise 5.
Each section contains some practical tips for the different parts of the exercise, and we have included some pseudocode for Parts 1 and 2 to help guide you in writing your code.
As a reminder, pseudocode is simply an explanation of what the code should do in plain English (or your language of choice).

## Part 1 - Reading and dividing the data file
### Pseudocode
1. Open the `816295.csv` data file for reading.
2. Read the values into a list where each list entry is one line of the file.
3. Loop over all lines in the resulting list (excluding the header). For each line:
  - Split the line into a list of values using the commas.
  - Extract the value for the year using the list item containing the date in the split line list above.
  - Create a varaible that is contains a character string of the name of the output file for that year (e.g., `"AA-1926.csv"`).
  - Open the file named above for writing.
  - Write the entire line to that data file.

### Practical tips
1. **Extracting the year for each line of the data file**.
In order to isolate the year when processing the data in the data file for this exercise, you need to use a substring, or part of a character string, from the values in column 6 of the `816295.csv` data file.
Those values have the form `YYYYMMDD` where `YYYY` is the year of the observation, `MM` is the month, and `DD` is the day.
You want to use only the year, and let's assume that for each line of the data file that is read, you assign the value in column 6 to a variable `date`.
The year part of `date` would then just be the first 4 characters in `date`, and since character strings are simply a list of characters, you can use the index values to extract a slice (or substring) from the variable `date`.
Since the first number in the year in `date` would simply be `date[0]`, and the last would be `date[3]`, all we need is a way to use only index values 0-3 in date.
You can access a range of index values in a string variable or list using the colon (`:`) character.
The example below may help make things more clear:

    ```python
    >>> text = "Helsinki"
    >>> print(text[0])
    'H'
    >>> print(text[3])
    's'
    >>> print(text[0:3]
    'Hel'
    ```
**Note**: Like the `range()` function, the last index value given in a range of values is not included in the list of indices.

## Part 2 - Calculating annual summer and winter temperatures
### Pseudocode
1. Create a list of names of all of the files generated in Part 1.
2. Loop over that list. For each file:
  - Open the file for reading.
  - Create two empty lists for storing the daily temperatures for summer and winter.
  - Loop over every 

## Part 3 - Saving your seasonal average files to GitHub
