AddressSanitizer: heap-buffer-overflow in __interceptor_memcpy
READ of size 1 at 0x61c000000708 thread T0

[Poc file](https://github.com/10cksYiqiyinHangzhouTechnology/tinydngSecurityIssueReport2/blob/main/id19)

[ASAN_tinydng](https://github.com/10cksYiqiyinHangzhouTechnology/tinydngSecurityIssueReport2/blob/main/asan_tinydng)

ASAN Report:
```bash
ubuntu@ubuntu:~/Desktop/tinydng/out/default/crashes$ ~/Desktop/tinydng/asan_tinydng id:000019,sig:11,src:000509,time:63211643,execs:13272738,op:havoc,rep:8
=================================================================
==3709290==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x61c000000708 at pc 0x55555558e4c0 bp 0x7fffffff2f90 sp 0x7fffffff2f80
READ of size 1 at 0x61c000000708 thread T0
    #0 0x55555558e4bf in stbi__get8 /home/ubuntu/Desktop/tinydng/stb_image.h:1557
    #1 0x55555558e4bf in stbi__tga_load /home/ubuntu/Desktop/tinydng/stb_image.h:5797
    #2 0x55555558e4bf in stbi__load_main /home/ubuntu/Desktop/tinydng/stb_image.h:1124
    #3 0x55555558f624 in stbi__load_and_postprocess_8bit /home/ubuntu/Desktop/tinydng/stb_image.h:1203
    #4 0x55555558fe00 in stbi_load_from_memory /home/ubuntu/Desktop/tinydng/stb_image.h:1373
    #5 0x5555555b1007 in tinydng::LoadDNGFromMemory(char const*, unsigned int, std::vector<tinydng::FieldInfo, std::allocator<tinydng::FieldInfo> >&, std::vector<tinydng::DNGImage, std::allocator<tinydng::DNGImage> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*) /home/ubuntu/Desktop/tinydng/tiny_dng_loader.h:5478
    #6 0x5555555ba586 in tinydng::LoadDNG(char const*, std::vector<tinydng::FieldInfo, std::allocator<tinydng::FieldInfo> >&, std::vector<tinydng::DNGImage, std::allocator<tinydng::DNGImage> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*) /home/ubuntu/Desktop/tinydng/tiny_dng_loader.h:4937
    #7 0x5555555baf87 in main /home/ubuntu/Desktop/tinydng/test.cpp:33
    #8 0x7ffff706b082 in __libc_start_main ../csu/libc-start.c:308
    #9 0x55555555dd6d in _start (/home/ubuntu/Desktop/tinydng/asan_tinydng+0x9d6d)

0x61c000000708 is located 0 bytes to the right of 1672-byte region [0x61c000000080,0x61c000000708)
allocated by thread T0 here:
    #0 0x7ffff7694587 in operator new(unsigned long) ../../../../src/libsanitizer/asan/asan_new_delete.cc:104
    #1 0x5555555c01bb in __gnu_cxx::new_allocator<unsigned char>::allocate(unsigned long, void const*) /usr/include/c++/9/ext/new_allocator.h:114
    #2 0x5555555c01bb in std::allocator_traits<std::allocator<unsigned char> >::allocate(std::allocator<unsigned char>&, unsigned long) /usr/include/c++/9/bits/alloc_traits.h:443
    #3 0x5555555c01bb in std::_Vector_base<unsigned char, std::allocator<unsigned char> >::_M_allocate(unsigned long) /usr/include/c++/9/bits/stl_vector.h:343
    #4 0x5555555c01bb in std::vector<unsigned char, std::allocator<unsigned char> >::_M_default_append(unsigned long) /usr/include/c++/9/bits/vector.tcc:635
    #5 0x5555555ba457 in std::vector<unsigned char, std::allocator<unsigned char> >::resize(unsigned long) /usr/include/c++/9/bits/stl_vector.h:937
    #6 0x5555555ba457 in tinydng::LoadDNG(char const*, std::vector<tinydng::FieldInfo, std::allocator<tinydng::FieldInfo> >&, std::vector<tinydng::DNGImage, std::allocator<tinydng::DNGImage> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*, std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >*) /home/ubuntu/Desktop/tinydng/tiny_dng_loader.h:4923
    #7 0x5555555baf87 in main /home/ubuntu/Desktop/tinydng/test.cpp:33
    #8 0x7ffff706b082 in __libc_start_main ../csu/libc-start.c:308

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/ubuntu/Desktop/tinydng/stb_image.h:1557 in stbi__get8
Shadow bytes around the buggy address:
  0x0c387fff8090: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c387fff80a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c387fff80b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c387fff80c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c387fff80d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c387fff80e0: 00[fa]fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c387fff80f0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c387fff8100: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c387fff8110: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c387fff8120: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c387fff8130: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
==3709290==ABORTING
```
