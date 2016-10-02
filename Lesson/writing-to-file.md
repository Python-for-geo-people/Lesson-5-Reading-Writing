# Writing data to a file

## Topics
- [Writing to a new file](#Writing-to-a-new-file)
- [Appending to a file](#append)
- [(Not) overwriting data files](#overwrite)
- [Useful functions related to filepaths](#4.Useful-functions-related-to-filepaths)
- [Copying contents from a file into another]()

## Writing to a new file

[Previous materials](reading-multiple-files.md) focused on reading data from file(s) but for sure it is as important to know how to write contents into a file. Writing data into a file uses the 
same `open` -function that we used for reading the data but when writing we use the `w` -mode.
  
1. When filepath is opened in write mode (`mode=w`), Python will create a file into that location. Let's create a file called `test.txt` into our home -folder:
   
  ```python
  # Let's store the filepath of the new file into a variable
  >>> out_file = '/home/geo/test.txt'
  
  # This will open the file in write -mode and create it at the same time
  >>> w = open(out_file, 'w')
  ```

Now the test.txt -file has appeared into our home -folder:

 ![New file was created](../img/new-file-writing.PNG)

2. We can of course write content into that file using `.write()` -function. Let's write a single line of text into our test file, and let's use the `with` -statement for opening the file \[0\]. 

   ```python
  # Open the file in write -mode 
  >>> with open(out_file, 'w') as w:
          # Write a line of text into that file
          my_line = "This is my first line of text written in Python!"
          w.write(my_line)
  ```

Now our test.txt file contains the line of text that we just wrote:

 ![First line of text](../img/first-line-of-text.PNG)

<a name="append"></a>3. We can also add stuff to already existing file using append -mode (`a`) in the open statement:
  
  ```python
  # Open the file in append -mode 
  >>> with open(out_file, 'a') as w:
          # Write a second line of text into our file
          second_line = "This is my SECOND line of text written in Python!"
          w.write(second_line)
  ```
  
Now our test.txt file contains the following:

 ![Second line of text](../img/second-line-of-text.PNG)
 
Hey, but wait a second. The text that we just added did not go to a new line! This happens because we did not say to the computer to add a new line after our write -statement. 
For doing that we need to add the `\n` -newline character at the end of each line that we write. Let's fix this.
  
<a name="overwrite"></a>4. We can overwrite the old contents of a file by opening it again in write -mode. **Notice:** this really does delete all the earlier contents of the file, so be careful! 
Let's write those two lines now with adding the new-line character at the end:

  ```python
  # This will now overwrite the old contents of the existing test.txt -file
  >>> with open(out_file, 'w') as w:
          # Write the first line of text but now with new-line character at the end
          my_line = "This is my first line of text written in Python!\n"
          w.write(my_line)
          # Write the SECOND line of text but now with new-line character at the end
          second_line = "This is my SECOND line of text written in Python!\n"
          w.write(second_line)
  ``` 
         
Now our test.txt file looks correct:

 ![Second line of text, correct](../img/second-line-of-text-fixed.PNG)

5. There is also another function called `.writelines()` that writes a list of texts into a file where each list item will be written into the output file. 
Let's add another two lines at once into our test.txt -file using writelines -function:
    
  ```python
  # Open the file in append -mode 
  >>> with open(out_file, 'a') as w:
          # Third and fourth lines of texts
          third_line = "This is my THIRD line of text written in Python!\n"
          fourth_line = "This is my FOURTH line of text written in Python!\n"
          
          # Write both of those lines at once
          w.writelines([third_line, fourth_line])
  ```

## 4. Useful functions related to filepaths

 - os.path.basename()
 - os.path.join()
 - os.path.isdir()
 - os.makedirs()
 - os.path.exists()

## Footnotes

- \[0\]: When reading / writing in Python, it is best to use the `with` -statement as it takes care of closing your file after you have read/written something into your file. *Closing* the file takes
care of saving the data into that file. If the file is not closed after writing something into it, the contents won't be saved into that file. It is similar idea than when thinking of writing something
into a Word template document but without saving it anywhere. You can find more info about how to write data without `with` -statement, and how to close files from **[here](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)**.   