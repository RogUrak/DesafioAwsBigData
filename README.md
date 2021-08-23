## (Bootcamp Dio) Creating a Big Data Ecosystem on AWS

This repository is part of the proposed activities in the Bootcamp Cognizant Cloud Data Engineer with focus in Data Engineering, taking the first steps in Python, Big Data and Cloud environment.

- **Basic requirements:**
  - Basic knowledge in Python, SSH and Linux;
  
  - AWS account. 
  
- **Objective:**
- Implement a cluster for distributed data processing using the AWS EMR service with Hadoop MapReduce to count words in a text file stored in AWS S3, through a Python algorithm.

- **Architecture:**

  - Python: MapReduce, MrJob;

  - Data Lake (S3): create temp, data and output folders;

  - EMR: Hadoop, Master, Nodes.


1. Access the link [https://aws.amazon.com/](https://aws.amazon.com/) and create an account;
2. Access Amazon S3 to *create a bucket* (data lake structure), naming as "yourBucketName";
3. Create a structure of folders: data / output / temp;
4. Access EC2, *Key pairs*, *create key pair* (yourKeyPairName) in *.pem format;
5. Access "*My security credentials*"
   - *Create new access key*, download .csv file, and close.
6. Go to Linux environment;
   - Create a Python virtual environment; 
     - *virtualenv --python=python3.9 venv_yourVenvFolderName*
     - *source venv_yourVenvFolderName/bin/activate*
7. Go to Amazon S3, folder 'data' -> upload -> *Add files -> 'sherlock.txt' (Source of this file: gutenberg.org/ebooks);
8. Go to Linux environment;
   - *nano ~/.mrjob.conf* (to edit the 'mrjob.conf' file);
     - Edit *aws_access_key_id*, and *aws_secret_access_key* (keys provided from the downloaded *.csv file when created the new access key); 
     - Rename *ec2_key_pair* to *yourKeyPairName*
     - Edit *ec2_key_pair_file* to *~/.ssh/*
     - Save and exit (Ctrl+o to save, Ctrl+x to exit)
   - *nano ~/.ssh/yourKeyPairName.pem* (to edit this file)
     - Paste the 'rsa private key'
     - Save and exit
   - *nano ~/.mrjob.conf* (to edit the 'mrjob.conf' file);
     - Edit *ec2_key_pair_file* to *~/.ssh/yourKeyPairName.pem*
     - Save and exit
   - Install two libraries;
     - boto3: *pip install boto3*
     - mrjob: *pip install mrjob*
   - Command to start Python algorithm;
     - *python wordcount.py -r emr s3://dio-live-datalake-rju/data/sherlock.txt --output-dir=s3://dio-live-datalake-rju/output/arq01 --cloud-tmp-dir=s3://dio-live-datalake-rju/temp/*
       - template: python *yourPythonFileName.py* -r emr *yourS3UriFromFileAddedInDataFolder* --output-dir=*yourS3UriFromOutputFolder/yourLogName* --cloud-tmp-dir=*yourS3UriFromTempFolder/* 
       - The results will be showed in files generated as '*yourLogName*' in the *output* folder.
