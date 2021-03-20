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
- Go to the tutorial directory.
```sh
cd ./condor_tutorial/
```
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
- Uncomment all lines in "test.R" by vi. See basic vi commands on Google.
```sh
vi test.py
```
- "R.cmd" files is for submitting R jobs to Condor. Let us look at the file.
```sh
cat R.cmd
```
Find the section for inputting the executable (which R/python) and arguments (your script).
```text
# this is the command or program you are running. 
# common executables and their locations are:
# R: /usr/bin/Rscript
# matlab: /opt/MatlabR2018a/bin/matlab 
# python 2.7.3: /opt/python/bin/python 
# python 3.4.4: /opt/python3.4/bin/python 
# many other applications can be found in /opt

executable = /usr/bin/Rscript  
arguments = test.R
```
Find the notification section and change the "username@gatech.edu" to your gt email account by vi.
```text
# these options will notify the email listed below if the job errors out or when it completes
# comment or delete these lines if you do not wish to get an email
# you will get an email for each instance of your job, so if you spawn 50 jobs you will get 50 emails.
notification = error
notification = complete
notify_user = username@gatech.edu
```
- Job submission.
```sh
condor_submit R.cmd
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
- For more advance functions, please refer to the official documentation (condor_tutorial.pdf) available in the directory.

## Upload and Download Files
- Upload Files.
```sh
scp ./local/dir/name.file username@castle.isye.gatech.edu:~/remote/dir/
```
- Download Files.
```sh
scp username@castle.isye.gatech.edu:~/remote/dir/name.file ./local/dir/
```
- For efficient files handling, please see [Cyberduck][1].


[1]:https://cyberduck.io

