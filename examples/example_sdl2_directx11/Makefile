#
# You will need SDL2 (http://www.libsdl.org):
#   brew install sdl2
#

#CXX = g++
#CXX = clang++

EXE = example_sdl2_dx11
IMGUI_DIR = ../..
SOURCES = main.cpp
SOURCES += $(IMGUI_DIR)/imgui.cpp $(IMGUI_DIR)/imgui_demo.cpp $(IMGUI_DIR)/imgui_draw.cpp $(IMGUI_DIR)/imgui_tables.cpp $(IMGUI_DIR)/imgui_widgets.cpp
SOURCES += $(IMGUI_DIR)/backends/imgui_impl_sdl2.cpp $(IMGUI_DIR)/backends/imgui_impl_dx11.cpp
OBJS = $(addsuffix .o, $(basename $(notdir $(SOURCES))))

LIBS = -framework Metal -framework MetalKit -framework Cocoa -framework IOKit -framework CoreVideo -framework QuartzCore
LIBS += `pkg-config --libs sdl2`
LIBS += -L/usr/local/lib -L/opt/local/lib $(IMGUI_DIR)/../dxmt/build/src/d3d11/d3d11.dylib $(IMGUI_DIR)/../dxmt/build/src/dxgi/dxgi.dylib $(IMGUI_DIR)/../dxmt/build/src/nativemetal/winemetal.dylib
LIBS += -Wl,-rpath,@loader_path/../../../dxmt/build/src/d3d11
LIBS += -Wl,-rpath,@loader_path/../../../dxmt/build/src/dxgi
LIBS += -Wl,-rpath,@loader_path/../../../dxmt/build/src/nativemetal

CXXFLAGS += `pkg-config --cflags sdl2`
CXXFLAGS += -I/usr/local/include -I/opt/local/include -I$(IMGUI_DIR)/../dxmt/include/native/directx -I$(IMGUI_DIR)/../dxmt/include/native/windows
CXXFLAGS += -std=c++17 -I$(IMGUI_DIR) -I$(IMGUI_DIR)/backends
CXXFLAGS += -Wall -Wformat
CFLAGS = $(CXXFLAGS)

%.o:%.cpp
	$(CXX) $(CXXFLAGS) -c -o $@ $<

%.o:$(IMGUI_DIR)/%.cpp
	$(CXX) $(CXXFLAGS) -c -o $@ $<

%.o:$(IMGUI_DIR)/backends/%.cpp
	$(CXX) $(CXXFLAGS) -c -o $@ $<

%.o:%.mm
	$(CXX) $(CXXFLAGS) -ObjC++ -fobjc-weak -fobjc-arc -c -o $@ $<

%.o:$(IMGUI_DIR)/backends/%.mm
	$(CXX) $(CXXFLAGS) -ObjC++ -fobjc-weak -fobjc-arc -c -o $@ $<

all: $(EXE)
	@echo Build complete

$(EXE): $(OBJS)
	$(CXX) -o $@ $^ $(CXXFLAGS) $(LIBS)

clean:
	rm -f $(EXE) $(OBJS)
