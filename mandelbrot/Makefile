PROGS := mandelbrot_gfortran mandelbrot_flang
GFORTAN_FLAGS := -Wall -pipe -O3 -fomit-frame-pointer -march=core2 -fopenmp
FLANG_FLAGS := -Wall -pipe -O3 -fomit-frame-pointer -march=core2 -fopenmp=libgomp

.phony: all clean test

all: $(PROGS)

clean:
	$(RM) $(PROGS)

test: $(PROGS)
	./mandelbrot_gfortran 200 | diff - mandelbrot-output.txt
	./mandelbrot_flang 200 | diff - mandelbrot-output.txt
	./mandelbrot_gfortran 1000 > out_gfortran.bin
	./mandelbrot_flang 1000 | diff - out_gfortran.bin
	./mandelbrot_gfortran 16000 > out_gfortran.bin
	./mandelbrot_flang 16000 | diff - out_gfortran.bin

mandelbrot_gfortran: mandelbrot.f90
	gfortran -o $@ $(GFORTAN_FLAGS) $^

mandelbrot_flang: mandelbrot.f90
	flang -o $@ $(FLANG_FLAGS) $^
