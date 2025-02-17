# SSDV

Simple command line app for encoding / decoding SSDV image data

Created by Philip Heron <phil@sanslogic.co.uk>  
http://www.sanslogic.co.uk/ssdv/

A robust packetised version of the `JPEG` image format.

Uses the Reed-Solomon codec written by Phil Karn, KA9Q.

## ENCODING

```shell
$ ssdv -e -c TEST01 -i ID input.jpeg output.bin
```

This encodes the `input.jpeg` image file into SSDV packets stored in the `output.bin` file.
`TEST01` (the callsign, an alphanumeric string up to 6 characters) and `ID` (a number from `0-255`) are encoded into the header of each packet.
The `ID` should be changed for each new image transmitted to allow the decoder to identify when a new image begins.

The output file contains a series of SSDV packets, each packet always being 256 bytes in length.
Additional data may be transmitted between each packet, the decoder will ignore this.

## DECODING

```shell
$ ssdv -d input.bin output.jpeg
```

This decodes a file `input.bin` containing a series of SSDV packets into the JPEG file `output.jpeg`.

## LIMITATIONS

Only JPEG files are supported, with the following limitations:

 - Greyscale or YUV/YCbCr colour formats
 - Width and height must be a multiple of 16 (up to a resolution of 4080 x 4080)
 - Baseline DCT only
 - The total number of MCU blocks must not exceed 65535

## INSTALLING

```shell
$ make
```

## TODO

* Allow the decoder to handle multiple images in the input stream.
* Experiment with adaptive or multiple huffman tables.
