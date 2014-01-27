RTL_FM scrito to send Efergy or Chacon Power Metter data to pilight

Based on:
---------

http://rtlsdr-dongle.blogspot.com.au/2013/11/finally-complete-working-prototype-of.html
http://goughlui.com/?p=5109

You need to use the generic-wattmeter pilight protocol (experimental)

https://github.com/1000io/pilight

Compile:
--------

gcc -lm -o EfergyRPI_efergy EfergyRPI_efergy.c

Execute using the following parameters:
---------------------------------------

nohup sudo rtl_fm -f 433500000 -s 200000 -r 96000 -g 30 2>/dev/null | /home/pi/efergy/EfergyRPI_pilight log2.csv
