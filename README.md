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
