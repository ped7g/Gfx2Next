# Gfx2Next

ZX Spectrum Next graphics conversion tool.

Converts an uncompressed 8-bit BMP or PNG file to the Sinclair ZX Spectrum Next graphics format(s).

## Supported Formats

* .nxb - Block
* .nxi - Bitmap
* .nxm - Map
* .nxp - Palette
* .nxt - Tiles
* .spr - Sprites
* .scr - Screens
* .tmx - [Tiled](https://www.mapeditor.org/)

## Usage

gfx2next [options] &lt;srcfile&gt; [&lt;dstfile&gt;]

## Options

|Parameter|Description|
|---|---|
|-debug|Output additional debug information|
|-font|Sets output to Next font format (.spr)|
|-screen|Sets output to Spectrum screen format (.scr)|
|-screen-noattribs|Remove color attributes|
|-bitmap|Sets output to Next bitmap mode (.nxi)|
|-bitmap-y|Get bitmap in Y order first. (Default is X order first)|
|-bitmap-size=XxY|Splits up the bitmap output file into X x Y sections|
|-sprites|Sets output to Next sprite mode (.spr)|
|-tiles-file=&lt;filename&gt;|Load tiles from file in .nxt format|
|-tile-size=XxY|Sets tile size to X x Y|
|-tile-norepeat|Remove repeating tiles|
|-tile-nomirror|Remove repeating and mirrored tiles|
|-tile-norotate|Remove repeating, rotating and mirrored tiles|
|-tile-y|Get tile in Y order first. (Default is X order first)|
|-tile-ldws|Get tile in Y order first for ldws instruction. (Default is X order first)|
|-tile-offset=n|Sets the starting tile offset to n tiles|
|-tile-offset-auto|Adds tile offset when using wildcards|
|-tile-pal=n|Sets the palette offset attribute to n|
|-tile-pal-auto|Increments palette offset when using wildcards|
|-tile-none|Don't save a tile file|
|-tile-planar4|Output tiles in planar (4 planes) rather than chunky format|
|-tiled|Process file(s) in .tmx format|
|-tiled-tsx|Outputs the tileset data as a separate .tsx file|
|-tiled-file=&lt;filename&gt;|Load map from file in .tmx format|
|-tiled-blank=n|Set the tile id of the blank tile|
|-tiled-output|Outputs tileset .png and map data to Tiled .tmx format|
|-tiled-width=n|Sets Tiled tileset width output in pixels (default is 256)|
|-block-size=XxY|Sets blocks size to X x Y for blocks of tiles|
|-block-size=n|Sets blocks size to n bytes for blocks of tiles|
|-block-norepeat|Remove repeating blocks|
|-block-16bit|Get blocks as 16 bit index for &lt; 256 blocks|
|-map-none|Don't save a map file (e.g. if you're just adding to tiles)|
|-map-16bit|Save map as 16 bit output|
|-map-y|Save map in Y order first. (Default is X order first)|
|-map-sms|Save 16-bit map with Sega Master System attribute format|
|-bank-8k|Splits up output file into multiple 8k files|
|-bank-16k|Splits up output file into multiple 16k files|
|-bank-48k|Splits up output file into multiple 48k files|
|-bank-size=n|Splits up output file into multiple n byte size files|
|-bank-sections=name,..|Section names for asm files|
|-color-distance|Use the shortest distance between color values (default)|
|-color-floor|Round down the color values to the nearest integer|
|-color-ceil|Round up the color values to the nearest integer|
|-color-round|Round the color values to the nearest integer|
|-colors-4bit|Use 4 bits per pixel (16 colors). Default is 8 bits per pixel (256 colors). Get sprites or tiles as 16 colors, top 4 bits of 16 bit map is palette index|
|-colors-1bit|Use 1 bit per pixel (2 colors). Default is 8 bits per pixel (256 colors)|
|-pal-file=&lt;filename&gt;|Load palette from file in .nxp format|
|-pal-embed|The raw palette is prepended to the raw image file|
|-pal-ext|The raw palette is written to an external file (.nxp). This is the default|
|-pal-min|If specified, minimize the palette by removing any duplicated colors, sort it in ascending order, and clear any unused palette entries at the end. This option is ignored if the -pal-std option is given|
|-pal-full|Generate the full palette for -colors-4bit mode|
|-pal-std|If specified, convert to the Spectrum Next standard palette colors. This option is ignored if the -colors-4bit option is given|
|-pal-none|No raw palette is created|
|-pal-rgb332|Output palette in RGB332 (8-bit) format|
|-pal-bgr222|Output palette in BGR222 (8-bit) format. Bits 7-6 are unused|
|-zx0|Compress all data using zx0|
|-zx0-screen|Compress screen data using zx0|
|-zx0-bitmap|Compress bitmap data using zx0|
|-zx0-sprites|Compress sprite data using zx0|
|-zx0-tiles|Compress tile data using zx0|
|-zx0-blocks|Compress block data using zx0|
|-zx0-map|Compress map data using zx0|
|-zx0-palette|Compress palette data using zx0|
|-zx0-back|Set zx0 to reverse compression mode|
|-zx0-quick|Set zx0 to quick compression mode|
|-asm-z80asm|Generate header and asm binary include files (in Z80ASM format)|
|-asm-sjasm|Generate asm binary incbin file (SjASM format)|
|-asm-file=&lt;name&gt;|Append asm and header output to &lt;name&gt;.asm and &lt;name&gt;.h|
|-asm-start|Specifies the start of the asm and header data for appending|
|-asm-start-auto|Sets start parameter for first item when using wildcards|
|-asm-end|Specifies the end of the asm and header data for appending|
|-asm-end-auto|Sets end parameter for first item when using wildcards|
|-asm-sequence|Add sequence section for multi-bank spanning data|
|-preview|Generate png preview file(s)|

## Examples
* gfx2next -tile-norotate -map-16bit -bank-16k -asm-z80asm -bank-sections=rodata_user,rodata_user,BANK_52,BANK_53,rodata_user -preview tiles.png
* gfx2next -tile-norotate -map-16bit -colors-4bit -asm-z80asm -bank-sections=rodata_user,BANK_17,BANK_17 tiles.png
* gfx2next -sprites -colors-4bit -pal-min -pal-ext -preview sprites.png
* gfx2next -bitmap -pal-std -preview titlescreen.png
* gfx2next -tiled-file=map.tmx -tile-norotate -map-16bit -pal-none -preview map_tileset.png
* gfx2next -tiled-output -tile-norotate -map-16bit -preview map.png
* gfx2next -tiled -tiled-blank=0 -tile-none -pal-none -zx0 *.tmx

## Source code
https://github.com/headkaze/Gfx2Next

## Compiling
gcc -O2 -Wall -o bin/gfx2next src/lodepng.c src/zx0.c src/gfx2next.c -lm

## Credits

* Ben Baker - [Gfx2Next](https://www.rustypixels.uk/?page_id=976) Author & Maintainer
* [Craig Hackney](https://github.com/iratahack) - Added -pal-rgb332 & -pal-bgr222, -colors-1bit, and -map-sms options and some fixes
* Einar Saukas - [ZX0](https://github.com/einar-saukas/ZX0)
* Jim Bagley - NextGrab / MapGrabber
* Juan J. Martinez - [png2scr](https://github.com/reidrac/png2scr)
* Lode Vandevenne - [LodePNG](https://lodev.org/lodepng/)
* Michael Ware - [Tiled2Bin](https://www.rustypixels.uk/?page_id=739)
* Stefan Bylund - [NextBmp / NextRaw](https://github.com/stefanbylund/zxnext_bmp_tools)

## Download
[Gfx2Next](https://www.rustypixels.uk/?download=1001)
