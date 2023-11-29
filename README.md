# A Simple Guide to Comparing database snapshots with diff

This guide will show you how to view database changes using snapshots and the diff command. This approach is particularly useful for Docker and Ubuntu environments.

## Step 1: Create a database snapshot before making any changes

The first step is to create a database snapshot that captures its current state. This can be done using the docker exec command and the mysqldump tool.
Bash

```bash
docker exec {container_name} /usr/bin/mysqldump -u {db_login} --password={db_password} --no-create-info --skip-triggers --skip-extended-insert --skip-opt --compact {db_name} > snapshot1.sql
```

This command will create a file called snapshot1.sql that contains a full dump of the database.

## Step 2: Make the desired changes to the database

Once you have a database snapshot, you can make the desired changes. You can add, edit, or delete records.

## Step 3: Create a second database snapshot after making the changes

After you have made the changes, create a second database snapshot. This will help you compare the changes made to the database.

```bash
docker exec {container_name} /usr/bin/mysqldump -u {db_login} --password={db_password} --no-create-info --skip-triggers --skip-extended-insert --skip-opt --compact {db_name} > snapshot2.sql
```

This command will create a file called snapshot2.sql that contains a dump of the database after the changes have been made.

## Step 4: Compare the two snapshots

Now you can use the diff command to compare the two snapshots. The diff command will compare two files and generate a list of all the differences between them.

```bash
diff --speed-large-files --suppress-common-lines snapshot1.sql snapshot2.sql
```

If you want to save the comparison results to a file, you can use the following command:

```bash
diff --speed-large-files --suppress-common-lines snapshot1.sql snapshot2.sql > result.sql
```

This command will create a file called result.sql that contains a list of all the differences between the two snapshots.

Additional Notes

    The -u and --password options are used to specify the database user and password.
    The -no-create-info option prevents the mysqldump command from creating a CREATE TABLE statement for each table in the database.
    The -skip-triggers option prevents the mysqldump command from including triggers in the dump.
    The -skip-extended-insert option prevents the mysqldump command from using extended INSERT statements in the dump.
    The -skip-opt option prevents the mysqldump command from optimizing the dump.
    The --speed-large-files option tells the diff command to use a faster algorithm for comparing large files.
    The --suppress-common-lines option tells the diff command to suppress output for lines that are the same in both files.

I hope this helps! Let me know if you have any other questions.
