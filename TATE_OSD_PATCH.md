# Tate OSD font/geometry patch

This fork contains an experimental fix for MiSTer's 90-degree OSD rotation.

## Change

In `sys/osd.v`, the MENU OSD header/title-strip geometry is now retained when `rot != 0`.

Previous:

```verilog
wire [21:0] osd_h_hdr = (info || rot) ? osd_h : (osd_h + OSD_HDR);
```

Patched:

```verilog
wire [21:0] osd_h_hdr = info ? osd_h : (osd_h + OSD_HDR);
```

The MENU framebuffer contains the title/header strip, so dropping `OSD_HDR` during Tate rotation can cause the rotated OSD sampling origin to be incorrect.

## Branch

`tate-osd-fix`

## Commit

`b42613c7720a8f298ba8600e16afa5019956ec87`

This is an experimental patch and should be tested on hardware for both rotation directions and normal orientation before being considered for upstream submission.
