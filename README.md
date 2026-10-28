# ZX Spectrum 48K Essentials

## Introduction

Sinclair ZX Spectrum 48K computer released in April 1982 was not the best one compared to its competitors but for sure became one of the most influential ones. A lot of hobbyists who nowadays collect, repair or mod Spectrum, might be tempted to create their own version - keeping the original idea/design that makes a Z80 system the Spectrum: ULA with its contended memory architecture, content of the ROM, original case and rubber keyboard but getting rid of all nonsenses where you could easily do better, even back then. 

It has to be said that this is not by any means revolutionary work. There are lots of similar projects and this one could easily be called Another Spectrum Clone but as mentioned before, every Spectrum lover would like to have his/her own version. I hope you like mine.

## Design

The idea is to leave all ZX Spectrum 48K components as they were originally and introduce only minimal changes. 

The main design decision concerns ULA. You might want to use original chip but it is difficult to get and you need to clone extensive analog video circuit (that occupies one third of the board) still getting relatively poor composite picture. On the other hand, you could use modern FPGA replacement that has RGB output - but this would not be ULA architecture (on the outside) any longer. I decided to use [vLA82S+](https://www.vretrodesign.com/products/vla82s-spectrum-ula-replacement-with-rgb-interface-and-ay-emulator-without-interface) by vRetro Design which is FPGA based ULA with RGB output but also a drop-in replacement for original chip so Sinclair's architecture will be preserved. Other changes are:
* Dynamically refreshed Lower RAM based on 4116 chips is replaced with more convenient static RAM which also allows to get rid of almost all of power supply section as -5V and +12V voltages are no longer needed. This is the solution commonly used in modern [memory replacements modules](https://www.retroleum.co.uk/spectrum-repairs-mods) – using set of flip-flops (74LS574) to hook up single RAM chip to raw/column address multiplexers used in original design.
  
* Dynamically refreshed Upper RAM 4132/64 chips use only one voltage, however they could easily be replaced with one 32KB static RAM chip. Memory type selection jumpers are no longer needed.
  
* While building your ZX Spectrum you probably will not source (difficult to get) original ROM but instead use modern EEPROM like W27C512 that you program with [content of the ROM](https://speccy4ever.speccy.org/_SIN.htm). ROM type jumpers are no longer needed.
  
* In power supply section efficient modern switching regulator is used that doesn't require a radiator. Also (as in MAX/Harlequin) bridge rectifier is added to save from mistakenly connecting power supply with wrong polarity (which from experience is likely to happen if you use more machines because Spectrum uses center-negative power jack while nowadays almost everything is center-positive).

Everything else is left intact.

## Parts

* Except for added components (marked with numbers 200+) all others <ins>have original references and are located in the same places</ins> on a PCB as in ZX Spectrum 48K Issue 3B. Four unmarked small elements are additional decoupling 100nF capacitors (P=2.5mm) for new ICs.
* Standard size 0,25W resistors are used, however compared to original their length is decreased from 0.6” to 0,5”. I really hate those banks of bus separation/pullup resistors so network ones are used wherever possible.
* Axial capacitors are used as in original design but you can install disc ones instead. I could not resist and left blue electrolytic capacitors (only two since there are no power and video sections), however there are mounting holes underneath (P=2.0mm) to use radial ones as well. 
* Original audio sockets are replaced with PJ-307 ones, commonly used in retro systems nowadays.
* Mini DIN8 connector (as in Harlequin 48K) is used to output RGB signal and mono sound to TV/monitor using [RGB Scart Lead cable](https://www.ebay.com/itm/253830448917?epid=17023035733&itmmeta=01JKTFD61QHFB48BB7ZDRB7SRS&hash=item3b19794715:g:KvwAAOSwlb5nn9B-).
* If you think using bridge rectifier is below you, shorten its pins: 1-4, 2-3 and don’t use it, but remember to use center-positive power supply!
* Be aware that 40 ohm speaker might be difficult to find.

## Board

Here is KiCad project of the board.

<img width="1362" height="890" alt="ZX48K-Essentials_board" src="https://github.com/user-attachments/assets/ee598e03-ff0a-4bd8-96da-728f28c4787b" />

Fully assembled ZX48essentials PCB, tested with [Diagnostic ROM](https://blog.retroleum.co.uk/electronics-articles/a-diagnostic-rom-image-for-the-zx-spectrum/), Kempston Pro Joystick Interface, [divMMC Future](https://www.tfw8b.com/product/divmmc-future-sinclair-zx-spectrum/), [ZX Interface 2](https://en.wikipedia.org/wiki/ZX_Interface_2) and [MaxDuino](https://lotharek.pl/productdetail.php?id=409).

<img src="ZX48K-Essentials_board_photo.jpg" />

## Remarks

* Because power section is severely reduced, only +5V (and now +9V) are available on edge connector. Also no video signals are present.
* If you intend to put the board in ZX Spectrum 48K case, vLA82S+ must be soldered. For ZX Spectrum 48K+ case you can use socket (standard not precision).
* Geoff Wearmouth's [Looking Glass ROM](https://drive.google.com/file/d/1Mf0jTW43AdGkd5ZbCQTpsrJHTxZ-JjuA/view) is worth checking.
* As a bonus, vLA82S+ has write-only AY-3-8910 compatible sound generator built-in. L and R channels are mixed and output as one to TV/monitor through mini DIN socket. If you connect microSD card interface that often has joystick port, you have everything you need :-)

## Update Oct 2026

Following changes has been made to PCB (now marked _version 3B_, previous version moved to subfolder):
* EAR and MIC sockets that were swapped are now in right places - noticed by @PaddyB64
* There are mounting holes for vLA82S+ video interface (if you have such a version, you don't have to supply and solder JST connector, DIN8 AV socket and R201-203) - suggested by @PaddyB64
* +9V that was previously missing has been added to edge connector.


Have fun!

Tomek

> [!NOTE]
> **Disclaimer**: This is my project that I’ve built and it works for me. You can do it as well but remember, you’re responsible for your own doings and the consequences, not me.
>
> **Licensed under**: CERN Open Hardware Licence Version 2 - Strongly Reciprocal. Read [CERN-OHL-S](https://ohwr.org/cern_ohl_s_v2.txt)
