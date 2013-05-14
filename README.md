psfex
=====

python and C codes to interpolate and reconstruct psfex images

using the python code
---------------------

    import psfex
    pex = psfex.PSFEx(filename)
    image = pex.get_rec(row, column)

using the C library
-------------------

    // this version uses the fits reading
    #include "psfex.h"
    #include "psfex_fits.h"

    struct psfex *psfex=psfex_fits_read(fname);
    struct psfex_image *im=psfex_rec_image(psfex,500., 600.);

    printf("rec[%ld,%ld]: %lf\n", row, col, PSFIM_GET(im, row, col));

    im=psfex_image_free(im);
    psfex=psfex_free(psfex);

using the standalone psfex-rec code
----------------------------------

This code will write out a fits file with the PSF image in it,
to be read by your favorite code.

    psfex-rec psfex_file output_file row col

The image will be in output_file

installation of python code
----------------------------

    git clone git@github.com:esheldon/psfex.git

    cd psfex

    # to install globally
    python setup.py install

    # to install in a particular place
    python setup.py install --prefix=/some/path

    # if you install in a prefix, make sure you
    # add the /some/path/lib/python2.7/site-packages
    # directory to your PYTHONPATH (replace python2.7
    # with your python version)

installation of C library and standalone psfex-rec code
------------------------------------------------------

    git clone git@github.com:esheldon/psfex.git

    cd psfex

    # to install globally
    make install

    # to install in a particular place
    make install prefix=/some/path

    # if you install in a prefix, make sure you
    # add the /some/path/bin to your PATH.
    #
    # also /some/path/lib # directory to your LD_LIBRARY_PATH and
    # LIBRARY_PATH.  Similarly add /some/path/include
    # to C_LIBRARY_PATH and CPATH


dependencies for python library
-------------------------------

- python 2.5 or greater
- numpy
- cfitsio

dependencies for C library
-------------------------------

- cfitsio
