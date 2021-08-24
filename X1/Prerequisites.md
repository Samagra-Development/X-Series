## Prerequisites
1. Install Docker [10 mins]
    1. [Windows](https://www.youtube.com/watch?v=5nX8U8Fz5S0#t=01m00s)
    2. [Mac OSX](https://docs.docker.com/get-docker/)
    3. [Linux](https://docs.docker.com/get-docker/)

2. Getting familiar with terminal [10 mins]
    1. [Windows](https://www.computerhope.com/issues/chusedos.htm)
    2. [Mac OSX](https://medium.com/@grace.m.nolan/terminal-for-beginners-e492ba10902a)
    3. Linux - Do you really need me to help you??

3. Setup PSQL on docker [10 mins]
    1. Test if docker is working fine using - `docker version` on your terminal. You should see something like this. ![MarineGEO circle logo](/X1/res/docker-version-output.png) 
    This will show the basic details and version of your engine that you can use to debug things later on.
    2. Create a new directory call `database` anywhere on you system. You can either test the 
    3. Add a new file called `docker-compose.yml` and add the contents of the [following file](https://gist.githubusercontent.com/ChakshuGautam/70184d2e8acacadb401eacfc2cc04acf/raw/c2ec25c8ee09b06f43ab3416efc9b8214873db8e/docker-compose.yml) into that.
    4. At this point your folder structure should look like this.
        ```txt
        database/
        ──── docker-compose.yml
        ```
    5. Open you terminal and [navigate to the directory](https://www.macworld.com/article/221277/command-line-navigating-files-folders-mac-terminal.html) that you created. You can check the currently directory using either the `pwd` or `cd ,`.
    6. Create your own instance of PSQL using this command `docker-compose up -d`. You should be able to see and output like this on your terminal. #TODO: Insert Image.
    7. Now open your Chrome and open the following url http://localhost:5001. Use the following key `2OWslm5aAjlTARU` to see your database.




## Importing Data to any PSQL Database via script 

### Prequisite

None

### Steps Involved

1. Creation of the Dataset to be imported<br />
 - This step can be done on Excel itself.<br />
 - Please check there are no spaces in the column headers (API will generate error, and also PSQL naming convention does not allow spaces in the column titles)<br />
 - Insert a blank row under the column titles<br />
 - This blank row contains the data types of the data under that column. Possible data types supported :-<br />
     **Integer** - If the data in the column are integers, then add int() in the cell under the column title. Please ensure there are no text/decimal entries in this column.<br />
     **Strings** - If the data in the column is text, then add varchar(255) in the cell under the column title. Please ensure that the length supported will be 255 characters.<br />
     **Decimal** - If the data in the column is of decimal format, then add decimal(m,n) in the cell under the column title. Here, **m** represents the length of the base and                        **n** represents the length of precision. *Please ensure there are no text entries in this column.<br />
     **Date** - If the data in the column is of date format, then add date(). Please ensure there are valid date format entries in this column.<br />
  - Save the file locally on your system as .csv<br />
       <br />
  2. Uploading of dataset<br /><br />
     **For Smaller Datasets (upto ~1 lakh rows), which can be easily uploaded on Google sheets**<br />
     - Import the sheet saved above on Google sheets.<br />
     - Please give edit access to *sql-cron-sheet@sql-automator.iam.gserviceaccount.com*<br />
     - Copy a link of the data range. This link will be used later when creating data for the script<br />

     **For Larger Datasets (>1 lakh rows), minio will be used to upload the data**<br />
     - Login to [Minio Browser](https://cdn.samagra.io/). Credentials are **username** : admin, **password**: cttsamagra<br />
     - Upload the csv on the Minio UI.<br />
     - Copy a link of this file. This link will be used later when creating data for the script<br />
     <br />
   3. Configuring the sheet/file on Scripts Sheet<br />
     - Open the [SQL Script Automation Sheet](https://docs.google.com/spreadsheets/d/1S8SnVgJtHe1u5Uz1sb99TvdIVqeipgCVFJ-N0NmCEMc/edit#gid=1290455573)<br />
     - Go to the sheet corresponding to your team, or create an invidual sheet by copying from existing sheet<br />
     - In your sheet, under the **PSQL Credentials(Slave)**, enter the database credentials where you want to upload this data<br />
     - To link the relevant data, enter the data range/file link under the column **Range to Copy**<br />
     - If file, then add then add **Link** under the column **Data type(sheet/link)**, else add **Sheet*<br />
     - If uploading from a google sheet, enter the name of the sheet tab under the **Sheet Name** column<br />
     - Enter the name of table to be created in the database under **Table Name** column. If a new table is to be created, follow the naming conventions similar to mentioned for 
       column titles above, else if trying add more rows, table name should be same to the table existing in database already<br />
     - **Everytime?** column is used when the sheet upload is automated, and represents if the row has to be run everytime the script is run in automated or not. The possible            responses are **Yes** or **No**.<br />
     - **Append** column represents if the data under the link is to append rows or destroy existing table and create the table again in database<br />
    <br />
   4. Running the script<br />
     - Go to [Postman Website](https://www.postman.com/). You might have to create an account there.<br />
     - Once logged in, Import the [collection](https://www.getpostman.com/collections/9fde9a45d1cf1959d5b3). You can refer this [link](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) to check out how to import collection.<br />
     - Once imported, you will see "Sql Import API" request.<br />
     - Under the request body, Replace the **sheet_id** key's value with ID of the sheet where you added the data in step (3) and Replace**sheet_name** key's valye with name of          the same sheet tab<br />
     - Once done, Click on **Send** button on top right.<br />
     - You should receive a response message as follows - {"status": "Queued"}<br />
     - You can also verify from the sheet, you should receive **SUCCESS**, or else error message will be printed on the top of the sheet tab.<br />
