INSTALL_DIR = /usr/lapack/

LIB = liblapacke.a cblas_LINUX.a

CXX = g++

all : lib/liblapacke.a

lib/libgfortran.a:
	cp /usr/lib/gcc/x86_64-linux-gnu/4.8/libgfortran.a lib/

lib/blas_LINUX.a:lib/libgfortran.a
	tar -xvf BLAS.tar.gz
	cd BLAS && make
	cp BLAS/blas_LINUX.a lib/
	rm -rf BLAS

lib/libcblas.a:lib/blas_LINUX.a lib/libgfortran.a
	tar -xvf cblas.tgz
	cp Makefile.in_of_cblas CBLAS/Makefile.in
	cd CBLAS && make
	cp CBLAS/lib/libcblas.a lib/
	cp CBLAS/include/cblas.h include/
	rm -rf CBLAS

lib/liblapacke.a:lib/libcblas.a lib/blas_LINUX.a lib/libgfortran.a
	tar -xvf lapack-3.5.0.tgz
	cp Makefile_of_lapack lapack-3.5.0/Makefile
	cp lapack-3.5.0/make.inc.example lapack-3.5.0/make.inc
	cd lapack-3.5.0/ && make
	cp lapack-3.5.0/*.a lib/
	cp lapack-3.5.0/lapacke/include/*.h include/
	rm -rf lapack-3.5.0

.IPHONY : install
install:lib/liblapacke.a lib/libcblas.a lib/blas_LINUX.a lib/libgfortran.a
	rm -rf $(INSTALL_DIR)
	mkdir $(INSTALL_DIR)
	mkdir $(INSTALL_DIR)include
	mkdir $(INSTALL_DIR)lib
	cp include/* $(INSTALL_DIR)include
	cp lib/* $(INSTALL_DIR)lib

.IPHONY : clean
clean:
	rm -rf $(INSTALL_DIR)
