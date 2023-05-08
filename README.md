# brooklyn-market-value

by Joe Hahn,<br />
joe.hahn@oracle.com,<br />
27 April 2023<br />
git branch=master

1 see blog post https://url.tbd

2 download data on Brooklyn property transactions from https://objectstorage.us-ashburn-1.oraclecloud.com/n/adwc4pm/b/OML_Data/o/brooklyn_sales.csv

3 that csv has columns borough & Borough and address & Address, which can cause confusion, so change those capitolized columns to Borough_, Address_

4 launch ADB instance, I used ADW having 2 ocpus

5 have ADB admin user load csv data into table admin.brooklyn_sales_raw

6 import OML notebook prep_data.json into OML, and execute. 

7 Note that Brooklyn transaction data does not include the propertys' latitude/longitude
coordinates. However it does include XCOORD and YCOORD, and
the following step (which is not described in the blog) uses the XCOORD,YCOORD data
plus the lat,long data for a few properties extracted from Google Maps,
to train ML models to estimate the lat,long of all properties. Eyeball comparisons of estimates
to actuals indicate that the error in this estimate is approximately a fraction of a city block,
which is good enough for tutorial purposes

8 import geolocate_addresses.json notebook into OML, and execute, to generate estimates
of each property's lat,long

9 navigate to AutoML and create an experiment that will predict the SALE_PRICE column
in your OML user's table brooklyn_train_filtered, with Case ID=Transaction_ID and
model metric=R2. Press Start > Better Accuracy to train ML model

10 import OML notebook validate_model.json into OML, and execute

11 deploy model as described in blog post

12 test deployed model per blog

13 import APEX application: log into your ADB's APEX workspace, then
click App Builder > Import f100.sql > Next > Next > Install

14 inspect APEX dashboards per blog

