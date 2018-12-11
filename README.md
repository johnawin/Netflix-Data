# Netflix-Dataset-Mapreduce-Job
https://docs.google.com/presentation/d/1a_qVuVOlCTfoMxohrMDNx9YfKv7YmffdY9a8CfTvuTI/edit#slide=id.p


Dataset: https://archive.org/details/nf_prize_dataset.tar


Execution time for finding the top 10 users by number of reviews submitted: 43 minutes and 25 seconds on local machine.

Execution time for finding the average rating for every movie and listing them least to greatest: 2 minutes and 19 seconds on local machine.


#README
Group Members: John Gers and Johnathan Nguyen
Steps:
1. 	Log into bridges by using the following command:

	ssh bridges.psc.xsede.org -p 2222

	Then, enter your xsede password and do any 2-factor authentication needed.

2. 	Once logged in, make a directory called project 4 by saying:

	mkdir project4

	Then, to go into the newly made directory:

	cd project4

3. 	Load into bridges all your text files and python files into directory project4.

	For ours:
	We chose to use the filezilla application.

4.	Once you have all of your files in project4, start hadoop by saying:

	interact -N 1 -t 01:00:00
	module load hadoop
	start-hadoop.sh

	and wait.

5. 	Once it is ready, run the following command to copy the previously made
	directory into hadoop:

	hadoop fs -put /home/username/project4

	Note: replace "username" with your xsede username

6. 	Run the following commands to run the mapreduce task on the respective text file.
 
	These commands will write the output to a respective text file.

	General:

	time hadoop fs python path/mapper.py | sort -k1,1 | python path/reducer.py | sort -k 2,2n > hadoop fs -appendToFile - path/output_textfile.txt

	For ours specifically:
  
  ****
  We couldn't get the files to load into the HDFS when they were stored on bridges so we had to run it locally using:
  time python /users/johngers/desktop/module3/mapper.py | sort -k 1,1| python /users/johngers/desktop/module3/reducer.py |sort -k 2,2n > /users/johngers/desktop/output2.txt
  ****

  This is the command that should have worked had we been able to load files into hadoop without errors:
	time hadoop fs python /home/johngers/project4/mapper.py | sort -k 1,1| python /home/johngers/project4/reducer.py |sort -k 2,2n > /home/johngers/project4/output2.txt

	Note:
	-k Option : Unix provides the feature of sorting a table on the basis of any column number by using -k option.
	Use the -k option to sort on a certain column. For example, use “-k 2” to sort on the second column.

7. 	To display the contents of the output text file run the following command:

	hadoop fs -cat output_filename.txt


Noteworthy command-line commands:

ls - List's items in current directory
cd - Changes to a new directory
mv - Moves files between two directories
cat - Display the contents of a text file
For bridges:
cd /home/username - will take you to your root directory
nano - Invoke the nano program in order to create text files. Ex. nano filename.extension
For hadoop:
hadoop fs -ls - lists your hadoop fs contents
hadoop fs -put filename.extension or directory - move the file or directory into hadoop
hadoop fs -cat output_filename.txt - displays the contents of a text file in command line

