## Linux Virus
1 virus lây nhiễm file x64 ELF viết bằng Assembly thực hiện kỹ thuật Reverse Text Segment

* Segment được mở rộng ngược lại 1 khoảng PAGE_SIZE để tạo khoảng trống chứa Virus.
* PAGE_SIZE nên được tính tùy theo từng TH, nhưng trong code này giả định là 4096 bytes.
* Lây nhiễm thư mục hiện tại (không lây nhiễm file đã bị lây nhiễm) và không chứa các đoạn mã nguy hiểm
* Entry point vẫn được giữ nguyên ở .text segment, khiến cho việc phát hiện khó hơn.

# BUILD

Được viết bằng FASM x64
```
$ fasm virus_elf.asm
flat assembler  version 1.73.32  (16384 kilobytes memory) 3 passes, 1123 bytes.

$ file virus_elf
virus_elf: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, no section header

$ echo -n 544d5a00 | xxd -r -p -s +0x9 - virus_elf

$ chmod 777 ./virus_elf
```
