include ../../config.mak

vpath %.c $(SRC_PATH)/modules/openhevc_dec

CFLAGS=$(OPTFLAGS) -I"$(SRC_PATH)/include" $(OSVC_CFLAGS)

ifeq ($(DEBUGBUILD), yes)
CFLAGS+=-g
LDFLAGS+=-g
endif

ifeq ($(GPROFBUILD), yes)
CFLAGS+=-pg
LDFLAGS+=-pg
endif

EXTRALIBS+=-L../../bin/gcc -L. -lgpac -lLibOpenHevcWrapper -lTLibVideoIO -lLibWrapper -lTLibDecoder -lTLibCommon -llibmd5 -lpthread $(OSVC_LDFLAGS)

#common obj
OBJS= openhevc_dec.o

SRCS := $(OBJS:.o=.c) 

LIB=gm_openhevc_dec.$(DYN_LIB_SUFFIX)


all: $(LIB)


$(LIB): $(OBJS)
	$(CXX) $(SHFLAGS) $(LDFLAGS) -o ../../bin/gcc/$@ $(OBJS) $(EXTRALIBS)

clean: 
	rm -f $(OBJS) ../../bin/gcc/$(LIB)

dep: depend

depend:
	rm -f .depend	
	$(CXX) -MM $(CFLAGS) $(SRCS) 1>.depend

distclean: clean
	rm -f Makefile.bak .depend



# include dependency files if they exist
#
ifneq ($(wildcard .depend),)
include .depend
endif