# GaTech ISyE HTCondor Tutorial
This repo provides a basic MacOS tutorial for using the high-throughput computing resource, HTCondor, at GaTech ISyE. 

## Tutorial Download 
- Access the server using terminal.
```sh
ssh username@castle.isye.gatech.edu
```
- Go to the directory you want to store the tutorial.
```sh
cd ./remote/dir/
```
- Clone this github repository.
```sh
git clone https://github.com/BillHuang01/condor_tutorial.git
```

## Run Scripts on Castle
- Run the python testing script. You will see "hello!" on terminal and a new text file "python_test1.txt" with text "hello world!". 
```sh
python3 test.py
cat python_test1.txt
```
- Run the R testing script. You will see "hello!" on terminal and a new text file "R_test1.txt" with text "hello world!".
```sh
Rscript test.R
cat R_test1.txt
```
- Remove all result text files.
```sh
rm *.txt
```

## Run Scripts using Condor
- Access to wren.
```sh
ssh wren.isye.gatech.edu
```
- Uncomment all lines in "test.py" and "test.R" by vi. See basic vi commands on Google.
```sh
vi test.py
```
- ".cmd" files is for submitting jobs to Condor. Let us look at the condor file.
```sh
cat python.cmd
```
Line 16 is to choose the executable, line 17 is to choose the script, and line 35 is for user notification. Change the "username@gatech.edu" to your gt email account by vi.
- Job submission.
```sh
condor_submit python.cmd
```
Three job files will be generated: log, output, and error.
- Check job status.
```sh
condor_q
```
- Remove job.
```sh
condor_rm $JOBID
```

