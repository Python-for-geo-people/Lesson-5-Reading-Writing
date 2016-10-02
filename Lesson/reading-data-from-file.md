# Reading data from a file
Our first task in this week's lesson is to learn how to read data from files.
In Python this comprises two tasks: (1) Opening the file to be able to read in the contents, and (2) reading in the contents of the file.
In terms of how the data is read, there are several options of which we will see two.
Later in the course you will be introduced to more sophisticated libraries that can help with reading data files, but for now we will focus on the traditional way in which data files can be read in Python.

The data used in this part of the exercise is from the [Smithsonian Institution's volcano database](http://volcano.si.edu/).

## Topics
- How to open files using `with`
- `file.read()`, `file.readline()`
- Splitting strings, escape characters, assigning to variables
- Skipping headers and other unwanted file data (comment lines, etc.)

## Downloading and extracting the data
1. You can start by downloading the [volcano data zip file](https://github.com/Python-for-geo-people/Lesson-5-Reading-Writing/raw/master/Data/volcano-data.zip) we will be using for this part of the lesson.
  - The Firefox browser will likely download the file to the `Downloads` directory in the home directory of your computer instance.
  If so, you should move the file into the home directory using the file browser.
2. Once you have moved the `volcano-data.zip` file into your home directory, you can unzip the file using the `unzip` command in the Terminal window.

    ```bash
    $ cd $HOME
    $ unzip volcano-data.zip
    $ ls volcano-data
    GVP-Volcano-Lat-Lon-Elev.csv GVP-Volcano-List.csv
    ```
You should now have a directory titled `volcano-data` in your home directory.
It contains two files based on [version 4.5.1 of the Smithsonian Institution's Holocene volcano database (updated 23.9.2016)](http://volcano.si.edu/list_volcano_holocene.cfm):
  - `GVP-Volcano-List.csv`: The complete Holocene volcano database file in `.csv` format and with header lines.
  **Note**: Values are separated by semicolons (`;`) in this version of the file rather than commas (`,`).
  - `GVP-Volcano-Lat-Lon-Elev.csv`: The volcano ID, latitude, longitude and elevation for the first 10 volcanoes in the Holocene volcano database.
  There are no headers in this file and values are separated by commas (`,`).

## Preparing to read the data files in **Spyder**
1. Let's start by opening **Spyder** by either double clicking on its icon on the Desktop or typing `spyder` in the Terminal window.
2. In order to use the data in the downloaded files, we need to change the working directory in **Spyder** to be the `volcano-data` directory in your home directory.
This can be done by clicking on the **File explorer** tab in the upper right pane of the **Spyder** window and navigating to the `volcano-data` directory.
3. After navigating to that directory, you should see the two data files. However, you also need to tell the IPython window in **Spyder** that the `volcano-data` directory is where we will be working.
This can be done by clicking on the button shown below to set the console's working directory to the one selected in the **File explorer**.

    ![Setting the Spyder directory](../img/Spyder-directory.png)<br/>
    *Setting the working directory for IPython in Spyder*.

We should now be ready to continue and start working with our data files.

## File reading option 1: Reading an entire file at once
There are several ways in which data can be read from a file in Python, but some are more common (or better in some cases) than others.
We will focus on two ways to read files that can be easily used for many types of data files.

1. We will begin by reading an entire file into a Python list.
To start we need to open the file for reading by typing the following into the **Spyder** editor:

    ```python
    with open("GVP-Volcano-Lat-Lon-Elev.csv", "r") as infile:
        <commands to read file...>
    ```
Here we are using the `open()` function in combination with the `with` statement in Python.
*I suppose an explanation is required*.
The general format used for opening files in Python is `open(<filename>, <mode>)`, where `filename` is the name of the file and `mode` is either `"r"` for reading a file or `"w"` for writing to a file.
In our case, we open our file (`"GVP-Volcano-Lat-Lon-Elev.csv"`) to be read (`"r"`).
In addition, we are using the `with` statement.
What this does is open our file and assign access to the file to a variable (`infile`).
Thus, using the variable `infile` we can access the file contents anywhere within the indented block of code beneath the `with` statement.
For instance, we will see how to read the file in the next point.
The main advantage of using the `with` statement is that normally you need to manually close file access in Python (using the `file.close()` method), but when using the `with` statement the file is automatically closed at the end of the indented block.
This ensures you don't forget to close it yourself.
Closing files is important because sometimes the final changes made to a file will not be written until the file is closed, for example.
2. With our file open, we can now proceed to read the file.

    ```python
    with open("GVP-Volcano-Lat-Lon-Elev.csv", "r") as infile:
        data = infile.read()
        print(data)
    ```
So what we have done here is to use the `file.read()` *method* to read in the entire file as one long character string.
What does that mean?
Well, this means that we now have a variable `data` that contains the entire contents of our data file (`GVP-Volcano-Lat-Lon-Elev.csv`).
Thus, if we save the script above as `readall.py` and run it in **Spyder**, we should see the following output to the IPython window:

    ```python
    210010,50.17,6.85,600
    210020,45.775,2.97,1464
    210030,42.17,2.53,893
    210040,38.87,-4.02,1117
    211001,43.25,10.87,500
    211003,42.6,11.93,800
    211004,41.73,12.7,949
    211010,40.827,14.139,458
    211020,40.821,14.426,1281
    211030,40.73,13.897,789
    ```
No surprises here, this looks like the contents of the `GVP-Volcano-Lat-Lon-Elev.csv` data file.
If you want to confirm, you're welcome to open that file in the **Spyder** editor.
Note that you may have to set **Files of type** to be "All files (\*)" in the **Open file** window to see the data files.
3. As mentioned, `file.read()` is a *method* for file objects that reads all data in as a single (potentially very long) character string.
You can confirm this using the `type()` function.

    ```python
    >>> type(data)
    str
    ```
Obviously, it is nice to read the entire file at once, but this may be a problem for very large data files that may not fit in memory on the computer.
4. To convert our character string `data` into a more usable format in which each line is a separate value in a Python list, we can use the `str.splitlines()` method.
Thus, we can create a list `datalist` that contains each line of the file as follows:

    ```python
    with open("GVP-Volcano-Lat-Lon-Elev.csv", "r") as infile:
        data = infile.read()
        datalist = data.splitlines()
        print(datalist)
    ```
Now each line of the data file will be a character string in the list `datalist`.
We can confirm this by running the example above, which should output the following to the IPython console:

    ```python
    ['210010,50.17,6.85,600', '210020,45.775,2.97,1464', '210030,42.17,2.53,893', '210040,38.87,-4.02,1117', '211001,43.25,10.87,500', '211003,42.6,11.93,800', '211004,41.73,12.7,949', '211010,40.827,14.139,458', '211020,40.821,14.426,1281', '211030,40.73,13.897,789']
    ```
We are now ready to start interacting with our file data.

## Interacting with file data
Once we have read the entire contents of a data file using `file.read()`, the resulting character string will need to be broken up into parts that can be assigned to variables for use in Python.

1. As we have seen, we currently have a 10-line-long data file stored in a character string as `data`.
In this form, we cannot directly interact with any of the values from the file.
We first need to separate the file into 


## File reading option 2: Reading an entire file line-by-line


## Pro tips
### Reading files using the `with` keyword
- Reading files using the `with` keyword
- `file.readlines()`
