GNSS-GPS-SDR
============

*NEWS:

14 Aug. 2014: Losing job. Finding new opportunity!

ADS-B out is verified by HACKRF --> air --> rtl-sdr dongle.

See adsb directory and video:

http://youtu.be/xpLDqBkUiKc  (out of China)

http://v.youku.com/v_show/id_XNzE4NzIzNDIw.html  (in China)

*Purpose:

Playing with GNSS/GPS by HACKRF and rtl-sdr SDR.

Type "make" to generate "gps_test" program.

--------------------------offline simulation--------------------------

gps_test gps_sig_tmp.bin 2.046e6 8.184e6 5000

gps_sig_tmp.bin can be generated by gps_sig_gen.m (MATLAB).

2.046e6: carrier frequency

8.184e6: sampling rate

5000: maximum frequency offset for frequency searching

gps_test gps.samples.1bit.I.fs5456.if4092.bin 4.092e6 5.456e6 5000

gps.samples.1bit.I.fs5456.if4092.bin can be downloaded: http://www.jks.com/gps/gps.html

-------------------------over the air test----------------------------

*playback gps.samples.1bit.I.fs5456.if4092.bin(http://www.jks.com/gps/gps.html)

run gps_bin1bit_log2bin.m to generate HACKRF playback file: gps.samples.8bit.IQ.fs5456.baseband.bin

use gps_Nottingham.grc to playback gps.samples.8bit.IQ.fs5456.baseband.bin

use rtl-sdr to capture signal: rtl_sdr -g 60 -f 1575.42e6 -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1575.42MHz.bin

use proc_rtl_bin_for_gps('rtl_2.8Msps_1575.42MHz.bin') to get 1bit bin to feed into gps_test program

see C/A result: gps_test rtl_2.8Msps_1575.42MHz_1bit.bin 0.62e6 2.8e6 100000

C/a results are equal to http://www.jks.com/gps/gps.html

*playback gps_sig_tmp_for_hackrf_tx.bin (generated by gps_sig_gen.m) to air by gps.grc.

test1:

capture air signal by:

rtl_sdr -g 60 -f 1574.8e6  -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1574.8MHz.bin

convert capture to 1bit bin file needed by gps_test:

proc_rtl_bin_for_gps('rtl_2.8Msps_1574.8MHz.bin'); (MATLAB)

RUN: gps_test rtl_2.8Msps_1574.8MHz_1bit.bin 0.62e6 2.8e6 100000

test2:

capture air signal by:

rtl_sdr -g 60 -f 1575.42e6 -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1575.42MHz.bin

convert capture to 1bit bin file needed by gps_test:

proc_rtl_bin_for_gps('rtl_2.8Msps_1575.42MHz.bin'); (MATLAB)

RUN: gps_test rtl_2.8Msps_1575.42MHz_1bit.bin 0.62e6 2.8e6 100000
