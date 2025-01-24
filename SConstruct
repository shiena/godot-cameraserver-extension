#!/usr/bin/env python

env = SConscript("godot-cpp/SConstruct")

env.Append(CPPPATH=["src/"])
sources = Glob("src/*.cpp")

library_path = "addons/CameraServerExtension/{}/libcameraserver-extension.{}{}"

if env["platform"] == "linux":
    env.ParseConfig("pkg-config glib-2.0 --cflags --libs")
    env.ParseConfig("pkg-config gio-2.0 --cflags --libs")
    env.ParseConfig("pkg-config libpipewire-0.3 --cflags --libs")
    sources += Glob("src/linux/*.cpp")
else:
    sources += Glob("src/dummy/*.cpp")

library = env.SharedLibrary(
    library_path.format(env["arch"], env["platform"], env["SHLIBSUFFIX"]),
    source=sources,
)

env.NoCache(library)
Default(library)
