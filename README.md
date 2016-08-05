# pipeline_collation_script
Python script to collate continuous gravitational wave search results and output search band and upper limit XML files.

This is a large, multi-purpose script. It's still being refactored, as it violates a number of DRY principles, making it potentially brittle.

This takes search results and compares these to frequency regions known to have serious data quality issues (from a vetoing procedure known as fscan, which identifies elevated non-stationary spectral lines). It checks that each search job has indeed been submitted and completed without error. Then it looks for the template (a fancy matched filter in N-dimensional parameter space) that has the highest detection statistic ('twoF'). It also produces an XML document of loudest twoF values in a designated frequency region, which is subsequently used to execute Monte-Carlo recovery of synthetic signals ('injections') to determine statistical upper limits, in the case of non-detection.

What is cool about this script, and what leads to a huge simplification in computational complexity over the use of blind hash tables, is the use of the bioinformatics library <a href="https://pypi.python.org/pypi/intervaltree">intervaltree</a>. The veto bands XML and search bands XML files are turned into interval trees, then their intersection is computed in <it>O</it>( Nlog(N) ). 

Thanks, biologists! 
