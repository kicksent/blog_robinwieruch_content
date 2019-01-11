+++
title = "How to setup PostgreSQL on MacOS"
description = "A installation guide for a PostgreSQL on MacOS setup for having a SQL database available on your OS. It comes with everything that's needed to connect a Node.js application to your database in JavaScript ..."
date = "2019-01-08T13:50:46+02:00"
tags = ["Node", "JavaScript"]
categories = ["Node", "JavaScript"]
keywords = ["postgres macos", "postgresql macos", "postgres setup", "postgresql setup", "postgres os setup"]
news_keywords = ["postgres macos", "postgresql macos", "postgres setup", "postgresql setup", "postgres os setup"]
hashtag = "#NodeJs"
card = "img/posts/postgres-sql-macos-setup/banner_640.jpg"
banner = "img/posts/postgres-sql-macos-setup/banner.jpg"
contribute = "postgres-sql-macos-setup.md"
headline = "How to setup PostgreSQL on MacOS"

summary = "The article is a checklist for myself, but for anyone else setting up PostgreSQL on MacOS."
+++

{{% sponsorship %}}

{{% pin_it_image "postgres macos" "img/posts/postgres-sql-macos-setup/banner.jpg" "is-src-set" %}}

This is a tutorial for setting up PostgreSQL 11 on MacOS. You might be wondering why there's a need for another setup guide for Postgres in the first place, since there are a few across the web. I found many tutorials and guides on how to set it up, but found most of them to be unclear and outdated, based on old PostgreSQL versions. The checklist is not comprehensive, though, as it is used for several tutorials on my website, I keep it updated with the recent versions of PostgreSQL. If you spot any flaws in this guide, a comment below the article would be very helpful to keep it up to date for other developers.

If you want to run PostgreSQL on Windows instead, you will find guidance over here: [How to setup PostgreSQL on Windows](https://www.robinwieruch.de/postgres-sql-windows-setup).

{{% chapter_header "PostgreSQL Installation on MacOS" "postgres-macos-installation" %}}

I recommend {{% a_blank "Homebrew" "https://brew.sh/" %}} for installing and managing applications on MacOS. It is installed using the following command in the MacOS terminal:

{{< highlight javascript >}}
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{{< /highlight >}}

The terminal runs through a series of installation operations, and will probably create folders in your local machine to accommodate Homebrews storage requirements. You can find more detailed instructions [here](https://www.robinwieruch.de/developer-setup/). After it's installed, update the Homebrew dependencies and install PostgreSQL on the command line:

{{< highlight javascript >}}
brew update
brew install postgresql
{{< /highlight >}}

Next, check your PostgreSQL version:

{{< highlight javascript >}}
postgres --version
postgres (PostgreSQL) 11.1
{{< /highlight >}}

The command line results will show the version you have installed on your local machine. I recommed using the latest version of libraries and software whenever possible to avoid compatibility issues with client-side applications.

{{% chapter_header "How to create a physical PostgreSQL Database" "postgresql-physical-database" %}}

Now you can initialize the physical space on your hard-disk to allocate databases. To do this, create a default *postgres* database on the command line in case it didn't happen automatically:

{{< highlight javascript >}}
initdb /usr/local/var/postgres
{{< /highlight >}}

You will see the error message: *"initdb: directory "/usr/local/var/postgres" exists but is not empty"* if the database was already created when you installed PostgreSQL. It means the folder where you are attempting to create a physical place for the database already has one. Either way, next you can move on to the next step.

When you connect to this physical database later, you will see an {{% a_blank "actual database" "https://stackoverflow.com/questions/50210158/whats-the-difference-between-initdb-usr-local-var-db-and-createdb-db" %}} which is called "postgres" as well. The postgres database is meant to be the default database for any third-party tools that you are using in combination with PostgreSQL. These tools attempt to make the default connection to this default database, so you shouldn't delete it.

{{% chapter_header "How to start/stop a PostgreSQL Database" "postgresql-start-stop" %}}

Let's see next how you can interact with the actual database. Manually start and stop your Postgres database server with the following commands:

{{< highlight javascript >}}
pg_ctl -D /usr/local/var/postgres start
pg_ctl -D /usr/local/var/postgres stop
{{< /highlight >}}

The terminal will confirm these operations with *"server started"* and *"server stopped"* feedback. You could also implement a script to start the server each time you boot up the machine, but I like to have control over when to start and stop my database server to avoid complications.

{{% chapter_header "How to create the actual PostgreSQL Database" "postgres-database" %}}

Next, let's go through the steps of setting up a database that can be used for one of your applications. Make sure the Postgre server is started first, then type these commands in the command line to create and remove a database:

{{< highlight javascript >}}
createdb mydatabasename
dropdb mydatabasename
{{< /highlight >}}

You can also connect to databases to execute SQL statements. Either use the `psql` command, or specify a database such as the default postgres database to connect:

{{< highlight javascript >}}
psql mydatabasename
{{< /highlight >}}

The command leads you to the psql shell, which you can exit by typing CTRL + d. In the psql shell, you can create and drop databases as well:

{{< highlight javascript >}}
CREATE DATABASE mydatabasename;
DROP DATABASE mydatabasename;
{{< /highlight >}}

To list all your databases, you can type `\list`. Your will see any new databases listed, as well as two default databases that come with postgreSQL called `template0` and `template1`. The templates should remain in your database list even if you aren't using them, as they may be useful later.

* \list - List all of your actual databases.
* \c mydatabasename - Connect to another database.
* \d - List the relations of your currently connected database.
* \d mytablename - Shows information for a specific table.

{{% read_more "PostgreSQL with Sequelize in Express Tutorial" "https://www.robinwieruch.de/postgres-express-setup-tutorial/" %}}