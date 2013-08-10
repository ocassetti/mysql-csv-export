mysql-csv-export
================

A simple tool to export the output of a mysql query into a
csv file.

## Description

Although there are tones of tools that export the result of a query
into csv file, I never found one you could run directly from the
a shell, i.e. non-graphic,  and get the output saved into a file. 
I work a lot of with DBAS (Database As a Service) such as Amazon RDS 
where it is not possible to use 

        SELECT INTO OUTFILE

Furthermore, SeLinux and AppAromor understandably prevent you from 
doing "SELECT INTO OUTFILE" in most cases.
Using phpmyadmin might be a good idea but this implies that you have
a machine where you can run phpmyadmin and it could also take a long
time to get a good and secure configuration. 

There are some solutions
http://stackoverflow.com/questions/356578/how-to-output-mysql-query-results-in-csv-format
that use a combination of sed and awk but as some noted 
> this will give you a tab separated file. Since commas (or strings
> containing comma) are not escaped it is not straightforward to change
> the delimiter to comma.

A solution that works really well, which is at the base of this little
tool, is to use a database connector and a proper library to parse the
CSV file. Pretty much all programming languages offer both database
connector and library to write CSV files. Good examples are Perl with
DBI and Text::CSV_XS packages or Ruby with csv and mysql2 gems.

In past two years I found myself writing variant of this concept many
and many times. So at the end I decided to write a simple too in Ruby 
to do the job. 

You can copy and adapt this tool to your needs, or just take the
concept and create similar tools in different languages.


## Dependencies 

The tool requires csv, optparse and the  mysql2 gem. The first two
should be installed by default in your ruby installation whereas
mysql2 might not be but it is very easy to obtain it: 
http://rubygems.org/gems/mysql2


## How to use it 
Put the mysql-export-csv somewhere in your PATH 

        mysql-export-csv --user <database username> \ 
	                 --password <database password> \
			 --host <database address> \
			 --database <database to execute the query> \
			 --output <file where to save the query> \
			 --query 'Query in SQL ' 
			 

## TODO

1. Handle exceptions and missing command line arguments
2. Handle connection exceptions 
3. Warn before overwriting existing csv files
4. Allow to specify different delimiters 


