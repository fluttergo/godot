# How to build 
> https://docs.godotengine.org/zh-cn/4.x/contributing/development/compiling/compiling_for_windows.html
> https://docs.godotengine.org/zh-cn/4.x/contributing/development/compiling/compiling_with_dotnet.html


#构建Editor for windows 以及 Windows导出模板

# Build editor binary
scons p=windows target=editor module_mono_enabled=yes
# Build export templates
scons p=windows target=template_debug module_mono_enabled=yes
scons p=windows target=template_release module_mono_enabled=yes

# Generate glue sources
bin/godot.windows.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue
# Build .NET assemblies
./modules/mono/build_scripts/build_assemblies.py --godot-output-dir=./bin --godot-platform=windows


#构建android导出模板
scons platform=android target=template_release arch=arm32
scons platform=android target=template_release arch=arm64
scons platform=android target=template_release arch=x86_32
scons platform=android target=template_release arch=x86_64
cd platform/android/java
# On Windows
.\gradlew generateGodotTemplates
# On Linux and macOS
./gradlew generateGodotTemplates