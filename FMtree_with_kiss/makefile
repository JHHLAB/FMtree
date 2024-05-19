CC = g++

# For program run

CC_OPTION = -fomit-frame-pointer -W -Wall -Winline -DNDBUG -O3 -mpopcnt -I../lib/kISS/include -std=c++20 -lspdlog -lfmt -mavx -mavx2 -mlzcnt -mbmi -ltbb -fopenmp

#CC_OPTION = -W -Wall -Winline -DNDBUG -O3 -mpopcnt -pg

# For debug
# CC_OPTION = -g -fomit-frame-pointer -W -Wall -Winline

ALL_OPS = tryall core Makeours Clear
ALL:$(ALL_OPS)

core:
	$(CC) -c bwt.cpp $(CC_OPTION)
tryall:
	$(CC) -c main.cpp $(CC_OPTION)
Makeours:
	$(CC) -o FMtree main.o bwt.o $(CC_OPTION)
Clear:
	rm *.o
     
      
