allantools
==========

A python library for calculating Allan deviation and related time & frequency statistics. GPL v3+ license.

Developed here https://github.com/aewallin/allantools, but also available on PyPi at https://pypi.python.org/pypi/AllanTools

Input data should be evenly spaced observations of either fractional frequency,
or phase in seconds. Deviations are calculated for given tau values in seconds.

These statistics are currently included:
* ADEV    Allan deviation
* OADEV   overlapping Allan deviation,
* MDEV    modified Allan deviation,
* TDEV    Time deviation
* HDEV    Hadamard deviation
* OHDEV   overlapping Hadamard deviation
* TOTDEV  Total deviation
* MTIE    Maximum time interval error
* TIERMS  Time interval error RMS

see /tests for tests that compare allantools output to other (e.g. Stable32) programs.
More test data, benchmarks, and comparisons to known-good algorithms are welcome.

Authors
=======
* Anders E.E. Wallin   anders.e.e.wallin "at" gmail.com
* Danny Price          https://github.com/telegraphic
* Cantwell G. Carson   carsonc "at" gmail.com

Installation
============

> sudo python setup.py install

Usage:
```python
import allantools # https://github.com/aewallin/allantools/
rate = 1/float(data_interval) # data rate in Hz
taus = [1,2,4,8,16] # tau-values in seconds
# fractional frequency data
(taus_used, adev, adeverror, adev_n) = allantools.adev(fract_freqdata, rate, taus)
# phase data
(taus_used, adev, adeverror, adev_n) = allantools.adev_phase(phasedata, rate, taus)

# notes:
#  - taus_used may differ from taus, if taus has a non-integer multiples of data_interval
#  - adeverror assumes 1/sqrt(adev_n) errors
```

Development
===========

To do:
* Stable32-style plots using matplotlib
* Modified Total variance
* Time Total (modified total variance scaled by (t^2/3) )
* Hadamard Total

Make sure your patch does not break any of the tests, and does not significantly reduce the readability of the code.

References
==========
http://en.wikipedia.org/wiki/Allan_variance

W.J.Riley, "THE CALCULATION OF TIME DOMAIN FREQUENCY STABILITY"
http://www.wriley.com/paper1ht.htm

Fabian Czerwinski, Matlab code
http://www.mathworks.com/matlabcentral/fileexchange/26659-allan-v3-0

M. A. Hopcroft, Matlab code
http://www.mathworks.com/matlabcentral/fileexchange/26637-allanmodified

Tom Van Baak
http://www.leapsecond.com/tools/adev_lib.c

SESIA I., GALLEANI L., TAVELLA P., Application of the Dynamic Allan Variance 
for the Characterization of Space Clock Behavior, 
http://dx.doi.org/10.1109/TAES.2011.5751232

S. Stein, Frequency and Time - Their Measurement and Characterization. 
Precision Frequency Control Vol 2, 1985, pp 191-416.
http://tf.boulder.nist.gov/general/pdf/666.pdf
       
S. BREGNI, Fast Algorithms for TVAR and MTIE Computation in Characterization of
Network Synchronization Performance. 
http://home.deib.polimi.it/bregni/papers/cscc2001_fastalgo.pdf

David A. Howe, The total deviation approach to long-term characterization
of frequency stability, IEEE tr. UFFC vol 47 no 5 (2000)
http://dx.doi.org/10.1109/58.869040
