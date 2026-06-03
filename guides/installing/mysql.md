Introduction
============

This article will guide you through the installation and configuration stages of MySQL for your particular Operating System. What is a MySQL database? [MySQL](/wikipedia:MySQL "wikilink") is a multi-user access database that stores a number of different kinds of information in scaleable tables. In layman's terms, it puts a bunch of stuff in charts for your server to read. rAthena no longer supports text based save files (for Accounts, Characters, etc.) and requires a MySQL database to create these save files.

Windows
-------

This guide will instruct you on installing MySQL on Windows Vista/7, although it should work relatively the same with Windows XP. This guide also assumes you have already [installed your rAthena server](/Installation_on_Windows "wikilink").
**<big>Uninstallation Note</big>**
Before continuing, it is important to note that if you make an error and decide to start again by uninstalling the MySQL database and software, that you make sure you do a *thorough* uninstallation, and then reboot Windows before trying again. A couple tips to make sure your uninstallation is thorough:

-   Uninstall Workbench first
-   Remove the MySQL database folders in your user folder. This is generally in:

`C:\Users\`<YOUR_USER_NAME>`\AppData\Roaming\MySQL `


and:

`C:\ProgramData\MySQL`


Just delete the whole folder.

-   Run Administrative Tools -&gt; Services and look to make sure nothing MySQL related is running or set to run (because it shouldn't exist anymore)
-   Go to the location on your hard drive you installed MySQL5 and Workbench and ensure everything is deleted.


Delete the whole MySQL folder.

-   Make sure you reboot.
-   There is a Oracle made guide [here](http://dev.mysql.com/doc/refman/5.1/en/windows-installer-uninstalling.html), but it isn't necessarily thorough.
-   If you still have hanging and crashing during the configuration wizard, you may have to create your root account manually. Do an internet search for this, as it varies by system. And continue afterwards at the "MySQL Workbench" section.

### Download

To install MySQL Server you will first need to download the package corresponding to your version of Windows. [MySQL Community Server](http://dev.mysql.com/downloads/mysql/) is available for free and is exactly what is needed. Version 5.5 currently works well with rAthena and is recommended. **ENSURE** that you download the appropriate bit version (32 or 64) for your system, if you do not, you will receive errors during the execution wizard. This software installs the server on your computer that stores the data files and tables. Although alone, without prior knowledge of MySQL it is very difficult to operate and configure your servers data. That is why you will need MySQL Workbench.
[MySQL Workbench](http://dev.mysql.com/downloads/workbench/5.2.html) is a tool for viewing your MySQL database in a GUI environment. As said, it is not required but very beneficial; in addition, it is required by this guide. To be able to install and run MySQL Workbench 5.2 your System also needs to have the libraries listed below installed. The listed items are provided as links to the corresponding download pages where you can fetch the necessary files.

[Microsoft .NET Framework 4 Client Profile](http://www.microsoft.com/download/en/details.aspx?id=17113)
[Microsoft Visual C++ 2010 Redistributable Package (x86)](http://www.microsoft.com/download/en/details.aspx?id=5555)

### Configure rAthena Files

Before you begin with your MySQL installation, you need to setup your server conf files to be ready for the database you are about to install. I choose to do this in advance, because it allows you to have the usernames and passwords ready for use so you don't have to go back and set them, and you can just run your server afterwards with everything all ready.

-   Open "inter_athena.conf", and change sql.db_password, char_server_pw, map_server_pw and log_db_pw to a password of your choice. For this guide we will use the password "Fish". Passwords are case sensitive. This is not a strong password, and you should use a better one, this is just an example. Also change log_db_db to "log". All other fields should be let alone, the default username and port functions fine. ([Image](http://imageshack.us/a/img546/9444/interathena.jpg))
-   Open "map_athena.conf" and "char_athena.conf" and locate the server communication passwords:

`userid: s1`
`passwd: p1`

Change these to whatever you want, but something secure. For this guide we will use "FishUser" and "FishPassword"

`userid: FishUser`
`passwd: FishPassword`

Make sure these are the same in both map_athena and char_athena otherwise you will have errors.

-   There are additional SQL configuration features in "login_athena.conf" that you should take a look at now, to enable for use (such as IPban features).
-   Write all these passwords down or keep the files open for reference and continue to your MySQL installation!

### Install MySQL

First, you will need to install the MySQL server where all the data will be stored. After downloading the [MySQL Community Server](http://dev.mysql.com/downloads/mysql/), run the installer and use the following steps (*for this installation version 5.5.28 was used*).

1.  Click next and accept the license agreement.
2.  Click "Typical" for Setup Type; then click "Install" (you may have to allow UAC control from windows).
3.  Click "Next" when the MySQL Enterprise tool pops up, this is a simple advertisement.
4.  After installation is finished the completion screen with a "Finish" button will show, make sure you have "Launch the MySQL Instance Configuration Wizard" **CHECKED**! The configuration wizard will allow you to setup the server to accept the kind of data you want and by setting it up now you will most likely never have to configure it again.
5.  Click "Next" at the first screen, and then click "[Standard Configuration](http://i.imgur.com/YlMPbm8.png)" and hit "Next".
6.  Check both "Install As Windows Service" and "Include Bin Directory in Windows PATH" for the Service Name, name it "*MySQL5*" and ensure "Launch the MySQL Server Automatically is **CHECKED**. ([Image](http://i.imgur.com/onQiIsh.png))
7.  On the next screen, you will need to select the root password. This password is very important as you will **never be able to retrieve it** so make sure you write it down somewhere safe. The "root" access to your MySQL database can pretty much do anything to your data, so make sure you keep this information safe. If you want to enable root access from a remote machine, check the included box. You probably won't need to enable that unless you know what you're doing. Keep the password you selected available for now.
8.  On the next screen just click "Execute" to run the configuration unless you want to go back and change something.
9.  Once it is finished, hit "Finish" to close the wizard. It will report if there are any errors (there shouldn't be).

### MySQL Workbench

Next it is time to install the MySQL Workbench application. This application will allow you to edit your database and prepare it for eAthena, as well as perform maintenance in the future.

1.  Run the MySQL Workbench installer and click "Next" on the first screen.
2.  Choose your installation directory. The default directory should be fine. Click "Next" to proceed.
3.  Select "Complete" and click "Next", and then install, granting permissions when prompted.
4.  Once the wizard is completed, hit "Finish" and the default Workbench screen will come up.
5.  This is called the Home Screen and should look like [this](http://i.imgur.com/iuSqaFC.png).
6.  You need to create a new server instance to host your files for rAthena to access. Select "New Server Instance" under the "Server Administration" section.
7.  A window will pop up, select "localhost" and click "Next". This installs the instance on the localhost, which is your computer.
8.  On the next screen, leave everything the default. Where it says "Username" leave that at root, so you have root access. Under that, click "[Store in Vault](http://i.imgur.com/3WD8m8b.png)" and enter the root password from earlier (it's alright to copy/paste the password if you put it in a text file).
9.  After it has successfully tested the database connection, click "Next"
10. On the next screen, leave the configuration settings defaulted. It should point to the existing service (MySQL5 from earlier) and the default path is fine. ([Image](http://imageshack.us/a/img600/1089/defaultwindowsconfig.jpg))
11. On the next screen hit "Next" and then "Continue" on the popup. Leave the Server Instance with the default name of

`mysqld@localhost`

You are now ready to install your rAthena databases.

### Database Installation

It is now time to install the pre-installed database files that will allow your rAthena server to connect to your MySQL database and properly store data, such as characters, items, and guilds. Open up MySQL Workbench to the home screen.

1.  Double click "localhost" on the left under the "SQL Development" section. ([Image](http://i.imgur.com/HwXFbe5.png))
2.  On the next screen (after a small loading bubble pops up), you will have access to the specific tables that were mentioned earlier. You will enter this screen in the future when you want to edit accounts and other things directly (not common).
3.  We need to install a new "Schema", this is like a folder where all the database tables are stored. [Click the yellow cylinder looking thing in the upper left to create a new Schema](http://i.imgur.com/70F2Ckl.png). Name it "ragnarok" - **NOTE!** Lower case is important here, make sure it is exactly "ragnarok". The server collation should be "Server Default".
4.  Click "Apply" to create the Schema. A window will pop up with the actual commands that are going to take place; click "Apply" again to finalize your order.
5.  Now right click 'ragnarok' under "Object Browser" and click "Set as default schema", a line will appear through it telling the browser that any commands you make now will be ordered to that Schema.
6.  Next, [click the button directly to the left of the one you just did](http://i.imgur.com/ntGId6y.png), it says "SQL" with a tiny folder. Navigate to your rAthena/sql-files/ folder, and open the sql script file "main.sql".
7.  You'll see a bunch of code appear, these are commands that will tell the browser to create plain databases for your rAthena server. Click the yellow lightning bolt in the upper left hand corner to execute it and allow it to finish (ensure you click the first lightning bolt, the one without a cursor symbol or a magnifying glass over it).
8.  After it finishes, a bunch of executed commands will appear on the bottom of the screen. You can now expand the ragnarok schema to see a bunch of tables. ([Image](http://i.imgur.com/GdUYaiU.png))
9.  Now, do the same thing for a schema called "log", but open and execute logs.sql instead of main.sql. Ensure the tables are there as well.
10. Close the existing query tabs by hitting the "X" in the upper right of the tab. With the ragnarok tables still open, scroll down to the "login" table and **RIGHT click** it, then select "Edit Table Data".
11. Here you'll see existing account information that players can log in with to make characters. If you remember, the first account is the server communication account and it has the default password that you were asked to reset earlier. For our example we chose "FishUser" and "FishPassword". Enter these in the "username" and "password" field. And then create your first GM account by clicking where the word "null" is on the row with a ' \* ' and enter "2000000" for the "account_id" field, with a username and password that you like. For this guide we chose a username of "AthenaGM" and a password of "12345" and a sex of "M". To enable full administrator GM, just set the "group_id" to "99". Zero out everything else. [When you are finished it should look like THIS](http://i.imgur.com/fgkz4uC.png).
12. Hit the "Apply" button in the corner and then again when the code prompt appears. This should modify your tables. After it is done, you may close the SQL Editor by clicking the "X" on the tab at upper left corner. Hitting the "X" in the upper right closes the whole workbench. If you accidentally close it, just open it again.
13. On the Workbench Home Screen, click "Manage Security" under Server Administration. Select "mysqld@localhost" and then click "OK".
14. The next screen is the security window. You want to add an account that your server can use to access the databases that is NOT the root account, for enhanced security. Click "Add Account" in the lower left of the default screen.
15. The login name needs to be "ragnarok", and the password we selected earlier for this guide is "Fish". The system will tell you how strong your password is... Fish is a very weak password. Leave the connectivity limit box defaulted and then hit "Apply" in the lower right. ([Image](http://i.imgur.com/00X2bQX.png))
16. You'll see the account show up in the left above root. Select it and then click the "Administrative Roles" tab.
17. Ensure that the "MonitorAdmin", "DBManager", "DBDesigner" and "BackupAdmin" are checked. Some of these will select themselves based on what you click. Then click "Apply". As a note, this step isn't entirely necessary but provides increased security. The simpler step is to just give the user all privileges by clicking the "DBA" option at the top. ([Image](http://i.imgur.com/fddQevd.png))
18. Click the "Schema Privileges" tab.
19. In this tab, click "ragnarok" and then click the only available button, which is "Add Entry...".
20. Leave "Any Host" selected and change Schema to "Selected Schemas". Then select the "ragnarok" schema and hit OK.
21. At the bottom, hit "Select 'ALL'" to enable all database privileges for this Schema. This allows your *ragnarok* user to have access to all the tables in the schema of the same name. In other words, it allows your server to read/write the tables in the database you made. Make sure you click "Save Changes".
22. Do the same for the "log" schema you made. When you are [done it should look like this](http://i.imgur.com/I2vfBbG.png).

**Congratulations!** You have successful installed the MySQL database and are ready to run your server! See below for further adjustments.

#### Additional Configurations

##### item_db and mob_db

Open your SQL editor by double clicking your connection under SQL development. Right click ragnarok, and set it as your default schema, then right click it again and choose "Alter schema...", then change collation from latin1 to utf8 - default collation.([Image](http://i.imgur.com/XLL88ew.png)) Then open item_db.sql and mob_db.sql(item_db_re.sql or mob_db_re.sql for Renewal servers) with a text editor, they are located in your sql-files folder, and select all of the text by either right clicking and choosing select all, or clicking edit and select all, then copy by doing basically the same thing for selecting but choose copy; you can also press and hold ctrl and C, then release. Now go back to the SQL editor, and in the white box below the tab that says SQL editor paste the contents of either item_db.sql or mob_db.sql (item_db_re.sql or mob_db_re.sql for Renewal servers), execute, and then do the other one and execute. ([Image](http://i.imgur.com/aK9CYNs.png)) Next, open inter_athena.conf in your conf folder, look for:

`//Use SQL item_db and mob_db for the map server`
`use_sql_db: no`

And change no to yes. Note that if you have a modified version of Athena such as 3CeAM you will have to manually add the modifications from the item_db in the db folder to your MySQL item_db, and also for mob_db. If you do not you will get errors when running your server.

##### Enabling Logging

Simply open log_athena.conf in your conf folder, and look for:

`// Use MySQL Logs? (SQL Version Only)`
`sql_logs: 0`

Change 0 to 1. You can also go through and change logging options. Your logs will be stored within your log schema. To view IPs in loginlog, you must click it, then right click it and choose alter table, then click on the columns tab. For the PK row, check all of the boxes, then apply it. Now you can double click on the loginlog and view the IPs, though after you are done alter the table again and uncheck all the boxes, this helps insure security. This should only be done for IP bans.

##### Increasing Security

**Use MD5 to encrypt your password**
\*\* **WARNING:** This will turn your passwords gibberish, just numbers and letters, making them unreadable so be sure to note down your password, either in a text file on your C drive, or on a piece of paper. In MySQL Workbench, click edit, then preferences, then click the SQL Queries tab. Uncheck "(Safe Updates) Forbid UPDATE and DELETE statements without a WHERE clause...", then click OK. Make ragnarok your default schema, by right clicking its name and clicking "Set as Default Schema", now click File, then Open SQL script, and open convert_passwords.sql. Then click the execute icon.

Linux
-----

To Install the Mysql Server there is really only a few things that you have to do.

### Installing MySQL

From your terminal, type

`sudo yum install mysql-server*`

- OR -

`sudo apt-get install mysql-server`

After your Operating System downloaded and installed MySQL, you will see your terminal window changed and you will be prompted to provide the root password for the MySQL server

### Setting up your own user

Once the server has been installed you will need to call the server from terminal with this command.

`mysql -u root`

or

`mysql -u root -p`

then, type in your password.

You are now logged into the MySQL server as root. The best way to use your own SQL server is to have a username of your own control with your own password. The next command will create your own user. The `IDENTIFIED` `BY` clause defines the password.

`CREATE USER 'ragnarok'@'%' IDENTIFIED BY 'ragnarok';`
`GRANT ALL PRIVILEGES ON 'ragnarok'.* to 'ragnarok'@'%' IDENTIFIED BY 'ragnarok';`
`flush privileges;`

If that doesn't work it my be due to a version syntax error, try the following.

      CREATE USER 'ragnarok'@'%' IDENTIFIED BY 'ragnarok';
      GRANT ALL PRIVILEGES ON ragnarok.* to 'ragnarok'@'%' IDENTIFIED BY 'ragnarok';

### Installing the Tables

      cd /path/to/rathena/

Note: Afterwards issue this command lines, please have your password prepared since every after command lines issued you will be prompted for it.

      mysql -u root -p ragnarok < main.sql

      mysql -u root -p ragnarok < logs.sql

      mysql -u root -p ragnarok < item_db.sql

      mysql -u root -p ragnarok < item_db2.sql

      mysql -u root -p ragnarok < item_db_re.sql

      mysql -u root -p ragnarok < item_db2_re.sql

      mysql -u root -p ragnarok < item_cash_db.sql

      mysql -u root -p ragnarok < item_cash_db2.sql

      mysql -u root -p ragnarok < mob_db.sql

      mysql -u root -p ragnarok < mob_db2.sql

      mysql -u root -p ragnarok < mob_db_re.sql

      mysql -u root -p ragnarok < mob_skill_db.sql

      mysql -u root -p ragnarok < mob_skill_db2.sql

      mysql -u root -p ragnarok < mob_skill_db_re.sql