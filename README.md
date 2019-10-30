
# SCImago Journal Sorting
This repo provides an ```.Rmd``` script, which uses [SCImago Journal data](https://www.scimagojr.com/journalrank.php?out=xls) to create costum journal libraries as static ```.html``` outputs, related to the original SCImago statistics.

# About SCImago Journal Rank

"*SCImago Journal Rank (SJR indicator) is a measure of scientific influence of scholarly journals that accounts for both the number of citations received by a journal and the importance or prestige of the journals where such citations come from. A journal's SJR is a numeric value indicating the average number of weighted citations received during a selected year per document published in that journal during the previous three years. Higher SJR values are meant to indicate greater journal prestige.*" (https://en.wikipedia.org/wiki/SCImago_Journal_Rank)

The data used in this overview is from https://www.scimagojr.com/journalrank.php

# Journal data

ATM The 2018 data is used and the table provided in this script is the download from SCImago with two changes in two chinese names deleting " to make the ```.csv``` readable. Here is the mail to SCImago describing the error:


> Dear scimagolab team,
> while working with this csv table https://www.scimagojr.com/journalrank.php?out=xls I came across that the count of rows does not match the count of 31971 entries which are provided in your overview. I was able to narrow down the whole thing and maybe you can adapt the changes in your data provided under the link above:
> The situation atm:
> Csv table
> Field sep = ;
> Strings provided as “string”
> Therefore, when a wrong “ is set somewhere, a following ; will be interpreted as string and line endings also (probably), ending up with as many lines as one entry until the next wrong “ appears.
> Testing with R:
```
download.file("https://www.scimagojr.com/journalrank.php?out=xls", destfile = "./srjdata.csv")
dat <- read.csv("./srjdata.csv", sep = ";")
```
> The ccode above loads a dataframe with 26665 entries but it should be 31971…
> In line 14771, of the csv table this entry exists
> ;"Chuan bo li xue" bian ji bu"; the “ in the middle of the name is clearly the first point where things go wrong…exactly until line 20462 where again a similar pattern appears: ;"Wei sheng yan jiu" bian ji bu"; again a “ in the middle of a string.
> After deleting those two “ , the import with R works. I am not sure if this is something because of encoding, mine is UTF-8 for the table. Maybe you can check if there is another possibility to use the “ sign in the names as they disrupt the table you are providing for some applications.
> Would be nice to hear if you changed it, since I use the download option in a script to get your up to date table, for choosing and sorting journals.
> Best regards and I like your platform :)
> Thorsten Höser

