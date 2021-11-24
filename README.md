# Tauron eLicznik Scraper

This Python 3 package allows to read electric energy meter reading history from the 
[Tauron eLicznik](https://elicznik.tauron-dystrybucja.pl/) website.


## Command line usage

With the package installed readings can be retrieved by simply running the `elicznik` command:
```
usage: elicznik [-h] [--format {raw,table,csv}] username password [date]

positional arguments:
  username              tauron-dystrybucja.pl user name
  password              tauron-dystrybucja.pl password
  date                  Date of data to be retrieved

optional arguments:
  -h, --help            show this help message and exit
  --format {raw,table,csv}
                        Specify the output format
```

Example
```
$ elicznik freddy@example.com secretpassword 10.7.2021
timestamp              consumed    produced
-------------------  ----------  ----------
2021-07-03 01:00:00       0.116       0
2021-07-03 02:00:00       0.105       0
2021-07-03 03:00:00       0.117       0
2021-07-03 04:00:00       0.108       0
2021-07-03 05:00:00       0.125       0
2021-07-03 06:00:00       0.11        0
2021-07-03 07:00:00       0.025       0.107
2021-07-03 08:00:00       0           1.058
2021-07-03 09:00:00       0.26        0.846
2021-07-03 10:00:00       0.034       1.326
2021-07-03 11:00:00       0           1.523
2021-07-03 12:00:00       0           1.166
2021-07-03 13:00:00       0           0.637
2021-07-03 14:00:00       0.677       0.482
2021-07-03 15:00:00       0.741       0.46
2021-07-03 16:00:00       0.031       0.284
2021-07-03 17:00:00       0           0.393
2021-07-03 18:00:00       0.051       0.058
2021-07-03 19:00:00       0.347       0.02
2021-07-03 20:00:00       0.378       0.021
2021-07-03 21:00:00       0.246       0
2021-07-03 22:00:00       0.213       0
2021-07-03 23:00:00       0.269       0
2021-07-04 00:00:00       0.138       0
```


## API usage

```
import datetime
import elicznik

m = elicznik.ELicznik("freddy@example.com", "secretpassword")
m.login()

readings = m.get_readings(datetime.date(2021, 7, 10))

for timestamp, consumed, produced in readings:
    print(timestamp, consumed, produced)
```


## TODO & bugs

* Add support for accounts with multiple meters
* Convert the dates to UTC and handle switches from and to DST properly
* Allow reading a date range instead of just one day
* Make the dependency on tabulate optional


## Similar projects

This project is based on the excellent
[tauron-elicznik-scrapper](https://github.com/MichalZaniewicz/tauron-elicznik-scraper) project by
[@Michał Zaniewicz](https://github.com/MichalZaniewicz), but there are several other available out there.

Among the other [similar eLicznik projects on GitHub](https://github.com/search?q=elicznik) there's one especially
worth checking out:
the [Tauron AMIplus sensor](https://github.com/PiotrMachowski/Home-Assistant-custom-components-Tauron-AMIplus) -- it's
an eLicznik Home Assistant integration.
