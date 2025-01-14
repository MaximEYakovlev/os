### OS

The file loader.s can be compiled into a 32 bits ELF object file with the following command:
```
nasm -f elf32 loader.s
```

The executable can now be linked with the following command:
```
ld -T link.ld -melf_i386 loader.o -o kernel.elf
```

Building an ISO image
```
mkdir -p iso/boot/grub
```
```
cp stage2_eltorito iso/boot/grub/
```
```
cp kernel.elf iso/boot/
```

The ISO image can then be generated with the following command:
```
genisoimage -R                              \
            -b boot/grub/stage2_eltorito    \
            -no-emul-boot                   \
            -boot-load-size 4               \
            -A os                           \
            -input-charset utf8             \
            -quiet                          \
            -boot-info-table                \
            -o os.iso                       \
            iso
```

Compiling C code.
The flags used for compiling the C code are:
```
-m32 -nostdlib -nostdinc -fno-builtin -fno-stack-protector -nostartfiles
-nodefaultlibs
```