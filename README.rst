DKB VISA QIF Exporter
=====================
The German bank DKB does not provide access to VISA transactions using HBCI, which is why this script has been written.

It will get you your DKB VISA transactions in the QIF format.

It has been inspired by Jens Herrmann's web_bank.py, but has been written using some newer tools/frameworks such as BeautifulSoup and mechanize, in the hope that it will be more stable against changes on the DKB web site.

Thanks to Jens Herrmann for the initial work nevertheless!

You may also be interested in the derived project `"dkbweb" by Tom <https://code.google.com/p/dkbweb/>`_ which provides additional features such as bank account transaction exporting.


How does it work?
-----------------
It will log-in as you at DKB's online banking website, will pretend to be
you, will use the CSV export feature and will convert the fetched data to
the QIF format, which can be imported by several financial tools.

Requirements
------------
You need Python >=2.7.x and mechanize. On current Ubuntu,
this should suffice:

    apt-get install python-mechanize

Usage
-----
    ./dkb.py --userid USER --cardid 1234 --output dkb.qif
    ./dkb.py --userid USER --cardid 1234 --from-date 01.01.2020 --output 1234.qif --cardid 2345 --from-date 02.02.2020 --output 2345.qif

with USER being the name you are using at the regular DKB online banking web site as well, with 1234 being the last four digits of your card (to select the proper card) and with dkb.qif being the output file.

You will be asked for a start date if you do not specify one using --from-date. Optionally, --to-date can be specified to further limit the time frame. If not given, it defaults to the current date.

Then you will be asked for your PIN and should get your dkb.qif file in the current directory after some informational output.

If it does not work, you may have mis-entered some of the required data or there may have been changes on the DKB web site, in which case adjustments to the script will be necessary.

The resulting QIF file can be imported in several financial tools, although I only tested GnuCash.  

To avoid entering PIN and doing two factor authentication multiple times, you also can specify multiple cardids with corresponding output files. In this case,
 - output and from-date are mandatory and must be specified for each cardid,
 - to-date and qif-account are optional and may be specified either for each cardid or not at all,
 - userid is mandatory and must be specified exactly once,
 - debug and raw and may be specified once or not at all, and
 - the first cardid argument is matched with the first output, from-date and possibly to-date and qif-account arguments, the second cardid argument with the second ouput, from-date, ... argument and so on.

If this script is of any help for you, please let me know. :)
