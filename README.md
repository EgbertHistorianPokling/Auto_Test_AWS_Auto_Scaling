# Auto_Test_AWS_Auto_Scaling
A testing tool for LSDE course assessment.

Uploading the test files to the AWS S3 bucket takes a long time since the S3 bucket and SQS queue must be manually emptied before the data can be uploaded, and the application's performance is difficult to reliably monitor.

Using the Python SDK, automated test scripts can be developed to efficiently and accurately test the application. Three scripts are used for automatic testing.

The first script is autoTest.py, which clears the storage bucket and uploads the test files in a particular directory. 

After the test files have been processed, getResultMsg.py is utilised. The script gets deleted messages from the wordfreq-results queue and reorganises and stores the messages in a new CSV file. 

The results message provides the task's start time and the time the message was delivered; the difference between the two timestamps indicates the task's running time. The runtimeParse.py script is mostly used to determine the runtime from a CSV file.

Once all the configuration is complete, the auto load test script needs to be run. The S3 bucket and SQS wordfreq-jobs queue have the files and messages when the test starts. When autoTest.py is run, the console will display the upload log. The storage bucket and queue are automatically cleared by running the script.

When the number of 'available messages' and 'running messages' is zero, all tasks are done, and the getResultMsg.py script may be performed. The result file name must be specified in the console, and the incoming messages will be displayed and saved in a CSV file. 

Finally, the knotted CSV file data are used to determine the runtime using the runtimeParse.py script. The console displays the overall load test runtime as well as the number of duplicate jobs, working instances, and failure warnings.
