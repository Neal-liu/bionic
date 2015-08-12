# Write malloc benchmark on bionic benchmark and run it on manta : 

cd bionic/benchmarks
/* write malloc benchmarks */
mm -B
adb push ~/android/out/target/product/manta/system/bin/bionic-benchmarks32 /data/local                
adb shell /data/local/bionic-benchmarks32 malloc

把上次的修改加進去比較效能：
cp -r libc/ libc_fix/
cd libc_fix/
patch -p2 < ../bionic-arm-clz.patch
cd bionic/benchmarks
mm -B LD_LIBRARY_PATH=../libc_fix/ LOCAL_MODULE_STEM_32=bionic-benchmarks32_fix
