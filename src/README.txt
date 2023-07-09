Name: Jimmy Tran
G#: G01130635
Course-Section: SWE645-001
Assignment: #1

Static Homepage (AWS S3):
http://swe645-assignment1-jtran51.s3-website-us-east-1.amazonaws.com/

Student Survey Form (AWS EC2 - Tomcat):
https://ec2-3-138-187-184.us-east-2.compute.amazonaws.com/jtran51_assignment1_part2/survey.html

For installation and setup, none is required to run the assignment.
The homepage is hosted on S3 and accessible publicly through
the given URL. The Survey form is hosted on an EC2 instance
and its URL is also provided on the homepage.

If you would like to host the source files on your own 
S3 and EC2 instance, follow these steps:

Installation Steps (AWS S3):
https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html#step5-upload-index-doc

    1) Create an S3 bucket
    2) Enable static website hosting
    3) Edit Block Public Access settings
    4) Add a bucket policy that makes your bucket content publicly available
    5) Configure an index document
		* upload provided index.html
		* upload provided GMU_logo.png to bucket
    6) Configure an error document
		* upload provided error.html
		* upload provided homer_simpson.GIF to bucket (optional)
    7) Test website endpoint
		* Buckets > Properties > Static website hosting > 
		click on the Bucket website endpoint
		
	You should now be able to host and access the homepage on 
	your own S3 bucket. To host and access the Survey form on
	EC2, follow these steps:
		
Installation Steps (AWS EC2):
	
	1) Find EC2 on AWS Console homepage and launch EC2 instance
	2) Choose 'Apache Tomcat packaged by Bitnami' as AMI
	3) Leave Instance type and details as default
	4) Leave storage as default
	5) Name your instance using the tag feature (optional)
	6) Leave Security Group configs default
	7) Upload or create key pair using AWS mgmt console
	8) Launch
	9) View your instance on the Amazon EC2 dashboard and
	find the public DNS address
	10) Using an FTP client and key pair, copy the provided 
	war file to /opt/bitnami/tomcat/webapps of the EC2 instance
	hosted at <public DNS address>
		* the war file contains survey.html, styles.CSS,
		and GMU_logo.png
	11) The survey form should now be deployed onto the EC2 instance
		a) The Tomcat homepage will be accessible through
		<public DNS address>
		b) The survey form should be accessible through
		<public DNS address>/<war file name>/<survey html file name>