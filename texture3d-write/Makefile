CFLAGS = -g -O3
BINARY = laplace2d
SRC = simpleGL3DSurfaceWrite  simpleGL3DSurfaceWrite_kernel
OBJSUFFIX=.o
OBJS = $(addsuffix $(OBJSUFFIX), $(SRC))
NVCC = nvcc
LIB=-lglut -lGLU -lGL -lcudart -lGLEW

all: $(BINARY)

$(BINARY): $(OBJS)
	$(CXX) $(CFLAGS) -o $(BINARY) $(OBJS) $(LIB)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

%.o: %.cpp
	$(CXX) $(CFLAGS) -c $< -o $@

%.o: %.cu
	$(NVCC) $(CFLAGS) -c $< -o $@

run: all
	time ./$(BINARY) 400 400 1e-5 1.6

clean:
	rm -rf $(BINARY) *.o

valgrind: all
	valgrind --leak-check=full ./$(BINARY) 400 400 1e-5 1.6
