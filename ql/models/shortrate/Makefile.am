
SUBDIRS = calibrationhelpers onefactormodels twofactormodels

AM_CPPFLAGS = -I${top_builddir} -I${top_srcdir}

this_includedir=${includedir}/${subdir}
this_include_HEADERS = \
    all.hpp \
    onefactormodel.hpp \
    twofactormodel.hpp

cpp_files = \
    onefactormodel.cpp \
    twofactormodel.cpp

if UNITY_BUILD

nodist_libShortRateModels_la_SOURCES = unity.cpp

unity.cpp: Makefile.am
	echo "/* This file is automatically generated; do not edit.     */" > ${srcdir}/$@
	echo "/* Add the files to be included into Makefile.am instead. */" >> ${srcdir}/$@
	echo >> ${srcdir}/$@
	for i in $(cpp_files); do \
		echo "#include \"$$i\"" >> ${srcdir}/$@; \
	done

EXTRA_DIST = $(cpp_files)

else

libShortRateModels_la_SOURCES = $(cpp_files)

endif

noinst_LTLIBRARIES = libShortRateModels.la

libShortRateModels_la_LIBADD = \
    calibrationhelpers/libCalibrationHelpers.la \
    onefactormodels/libOneFactorModels.la \
    twofactormodels/libTwoFactorModels.la

all.hpp: Makefile.am
	echo "/* This file is automatically generated; do not edit.     */" > ${srcdir}/$@
	echo "/* Add the files to be included into Makefile.am instead. */" >> ${srcdir}/$@
	echo >> ${srcdir}/$@
	for i in $(filter-out all.hpp, $(this_include_HEADERS)); do \
		echo "#include <${subdir}/$$i>" >> ${srcdir}/$@; \
	done
	echo >> ${srcdir}/$@
	subdirs='$(SUBDIRS)'; for i in $$subdirs; do \
		echo "#include <${subdir}/$$i/all.hpp>" >> ${srcdir}/$@; \
	done

