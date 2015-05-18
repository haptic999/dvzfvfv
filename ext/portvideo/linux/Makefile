TARGET = reacTIVision
CSOURCES = $(shell ls ../ext/libfidtrack/*.c ../common/*.c)  
COBJECTS = $(CSOURCES:.c=.o)
CPPSOURCES = $(shell ls ./*.cpp ../common/*.cpp ../interface/*.cpp) 
CPPOBJECTS = $(CPPSOURCES:.cpp=.o)

SDL_CFLAGS  := $(shell sdl2-config --cflags)
SDL_LDFLAGS := $(shell sdl2-config --libs)

INCLUDES = -I../common -I../interface
COPTS  = -Ofast -w
CDEBUG = -Wall -g
CFLAGS = $(COPTS) $(SDL_CFLAGS) $(INCLUDES) -DLINUX -DNDEBUG
#CFLAGS = $(CDEBUG) $(SDL_CFLAGS) $(INCLUDES) -DLINUX
CXXFLAGS = $(CFLAGS)

LIBS = $(SDL_LDFLAGS) -ldc1394 -lpthread -lturbojpeg

all:	$(TARGET) 

$(TARGET) : $(CPPOBJECTS) $(COBJECTS)
	$(CXX) -o $@ $+ $(LIBS) 

clean:
	rm -f $(TARGET) $(CPPOBJECTS) $(COBJECTS) core*

run:	$(TARGET)
	./$(TARGET)

install: $(TARGET)
	install -d $(DESTDIR)$(BINDIR)
	install -m 755 -c $(TARGET) $(DESTDIR)$(BINDIR)
	install -m 644 -c ../README.txt $(DESTDIR)$(PREFIX)/share/$(TARGET)
	install -m 644 -c ../LICENSE.txt $(DESTDIR)$(PREFIX)/share/$(TARGET)
	install -m 644 -c ../CHANGELOG.txt $(DESTDIR)$(PREFIX)/share/$(TARGET)
	install -d $(DESTDIR)$(PREFIX)/share/applications/
	install -m 666 -c *.desktop $(DESTDIR)$(PREFIX)/share/applications/
	install -d $(DESTDIR)$(PREFIX)/share/pixmaps/
	install -m 666 -c *.png $(DESTDIR)$(PREFIX)/share/pixmaps/
	install -d $(DESTDIR)$(PREFIX)/share/icons/hicolor/128x128/apps/
	install -m 666 -c *.png $(DESTDIR)$(PREFIX)/share/icons/hicolor/128x128/apps/
	install -d $(DESTDIR)$(PREFIX)/share/icons/hicolor/scalable/apps/
	install -m 666 -c *.svg $(DESTDIR)$(PREFIX)/share/icons/hicolor/scalable/apps/