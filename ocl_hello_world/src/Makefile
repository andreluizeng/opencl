#before buildint it don't forget to export ROOTF_DIR and TOOLCHAIN (only if they are uncommented here)

# needs to source /opt/poky/x.x.x/environmentsetup.sh
APPNAME			= cl_helloworld
DESTDIR			= ../bin
SRCDIR			= ../src

DEL_FILE		= rm -rf
CP_FILE			= cp -rf    

ROOTFS_DIR = $(SDKTARGETSYSROOT)

TARGET_PATH_LIB 	= $(ROOTFS_DIR)/usr/lib
TARGET_PATH_INCLUDE 	= $(ROOTFS_DIR)/usr/include


CFLAGS			= -DLINUX -DUSE_SOC_MX6 -Wall -O2 -fsigned-char -march=armv7-a -mfpu=neon -mthumb-interwork -mtune=cortex-a9 -mfpu=vfp -mfloat-abi=hard \
			  -DEGL_API_FB -DGPU_TYPE_VIV -DGL_GLEXT_PROTOTYPES -DENABLE_GPU_RENDER_20 \
			  -I. -I$(TARGET_PATH_INCLUDE) \
                          -I$(TARGET_PATH_INCLUDE)/glib-2.0 -I$(TARGET_PATH_LIB)/glib-2.0/include \
                          -I$(TARGET_PATH_INCLUDE)/libxml2 \

LFLAGS			= -Wl,--library-path=$(TARGET_PATH_LIB),-rpath-link=$(TARGET_PATH_LIB) -lm \
			   -lCLC -lOpenCL -lpthread



OBJECTS			= $(APPNAME).o

first: all

all: $(APPNAME)

$(APPNAME): $(OBJECTS) 
	$(CXX) $(LFLAGS) -o $(DESTDIR)/$(APPNAME) $(OBJECTS)  

$(APPNAME).o: $(APPNAME).cpp
	$(CXX) $(CFLAGS) -c -o $(APPNAME).o $(APPNAME).cpp
	

clean:
	$(DEL_FILE) $(SRCDIR)/$(OBJECTS)
	$(DEL_FILE) $(DESTDIR)/$(OBJECTS)
	$(DEL_FILE) $(DESTDIR)/*~ $(DESTDIR)/*.core
	$(DEL_FILE) $(DESTDIR)/$(APPNAME)
	
distclean: clean
	$(DEL_FILE) $(DESTDIR)/$(APPNAME)

install: all
	#${CP_FILE} $(SRCDIR)/$(APPNAME) $(DESTDIR)/$(APPNAME)
	#${CP_FILE} $(DESTDIR)/$(APPNAME) $(ROOTFS_DIR)/home/opencv

