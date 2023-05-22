# brooklyn-market-value

by Joe Hahn,<br />
joe.hahn@oracle.com,<br />
27 April 2023<br />
git branch=master

1 see blog post https://url.tbd

2 download zipped data from https://www.kaggle.com/tianhwu/brooklynhomes2003to2017 and unzip to your desktop

3 that csv has columns borough & Borough and address & Address, so change those capitolized columns to Borough_, Address_
to avoid any confusion.

4 Also change name of first column to transaction_id

5 launch ADB instance, I used 2ocpu ADW version 19c

6 have ADB admin user load csv data into table admin.brooklyn_sales_map

7 have admin user create ADW user MLUSER

8 have admin user grant user MLUSER select access to table admin.brooklyn_sales_map:

    grant select on admin.BROOKLYN_SALES_MAP to MLUSER;

9 grant MLUSER permission to create tables

    grant create table to MLUSER;

10 import OML notebook prep_data2.json into OML, and execute. 

11 Note that Brooklyn transaction data does not include the propertys' latitude/longitude
coordinates. However it does include XCOORD and YCOORD, and
the following step (which is not described in the blog) uses the XCOORD,YCOORD data
plus the lat,long data for a few properties extracted from Google Maps,
to train ML models to estimate the lat,long of all properties. Eyeball comparisons of estimates
to actuals indicate that the error in this estimate is approximately a fraction of a city block,
which is good enough for tutorial purposes

12 import geolocate_addresses.json notebook into OML, and execute, to generate estimates
of each property's lat,long

13 navigate to AutoML and create an experiment that will predict the SALE_PRICE column
in your OML user's table brooklyn_train_filtered, with Case ID=Transaction_ID and
model metric=R2. Press Start > Better Accuracy to train ML model

13 import OML notebook validate_model.json into OML, and execute

14 deploy model as described in blog post

15 test deployed model per blog

16 import APEX application: log into your ADB's APEX workspace, then
click App Builder > Import f100.sql > Next > Next > Install

17 inspect APEX dashboards per blog

