pilight-pimatic-efergy
----------------------

RTL_FM script to read and send Efergy or Chacon Power Metter data to pilight or pimatic

Based on
--------

http://rtlsdr-dongle.blogspot.com.au/2013/11/finally-complete-working-prototype-of.html

http://goughlui.com/?p=5109

You need to use the generic-wattmeter pilight protocol (experimental)

https://github.com/1000io/pilight

Compile
-------

gcc -lm -o EfergyRPI_efergy EfergyRPI_efergy.c

Execute & Save Log Archive
--------------------------

nohup sudo rtl_fm -f 433500000 -s 200000 -r 96000 -g 30 2>/dev/null | /home/pi/efergy/EfergyRPI_pilight log2.csv

Log Example
-----------

[date],[time],[wats],[euros]

date:03/09/16,22:42:15,wat:283.198242,euro:0.035400
date:03/09/16,22:42:21,wat:285.585938,euro:0.035698

Pimatic Integration
-------------------

You can use it with pimatic-log-reader as I do :)

https://pimatic.org/plugins/pimatic-log-reader/

pimatic config example:

    {
      "id": "WattMeter",
      "name": "Consumo Watts",  //sensor display name
      "class": "LogWatcher",
      "file": "/home/pi/EfergyRPI/log_efergy.csv",  //log file
      "attributes": [
        {
          "name": "watts",
          "type": "number",
          "unit": "W"
        },
        {
          "name": "euros",
          "type": "number",
          "unit": "€"
        }
      ],
      "lines": [
        {
          "match": "date:(.+),(.+),wat:(.+),euro:(.+)",
          "watts": "$3",
          "euros": "$4"
        }
      ]
    }

Thanks to
---------
  
@Nathaniel Elijah
@Gough Lui
