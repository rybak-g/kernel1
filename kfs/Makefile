CFLAGS += -nostdinc -fno-builtin -m32
CFLAGS += -fno-stack-protector -Wall -Wextra
ASFLAGS += -m32
LDFLAGS += -nostdlib -m32 -Wl,--build-id=none

all: kernel.bin

kernel.bin: src/printk.o src/crt0.o src/vfb.o src/string.o src/main.o
	ld -melf_i386 -T kfs.ld -o kernel.bin src/printk.o src/crt0.o src/vfb.o src/string.o src/main.o

clean:
	rm -f src/*.o kernel.bin

boot: all
	qemu-system-x86_64 -kernel kernel.bin -serial stdio -nographic -monitor pty
#boot the kernel using Qemu or Bochs.

debug:
	qemu-system-x86_64 -kernel kernel.bin -s -S
#boot the kernel and attach a gdb on it.
