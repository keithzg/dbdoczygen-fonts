# Dbdoczygen Font

Oxygen Font is a project to design a desktop/gui font for integrated use with the KDE desktop.

The basic concept for Oxygen Font is to design a clear, legible, sans serif font which would be rendered with Freetype on Linux-based devices. In addition a bold weight and a monospace version were made.

G. Michaels Consulting Ltd. then wanted slashes on the zeroes and then some changes to the monospace height cutoff, and so here we are, with a "new" font named Dbdoczygen.

## Requirements

You'll need at least FontForge, as well as `eot-utils` (that's the *buntu package, at least) for the EOT output and `woff2_compress` (from the woff2 package). On Debian or Ubuntu, then, you should run:

```
apt install fontforge eot-utils woff2
```

## Design

Oxygen, the basis for Dbdoczygen, was to be constructed closely with the gridfitting aspects of the Freetype engine. The fonts were to also be autohinted with Werner Lemberg's "ttfautohint" library to further the compatibility with the Freetype engine. The aim of this approach was to produce a family of freetype-specific desktop fonts whose appearance would stay uniform under different screen render settings, unlike more traditionally designed 'screen fonts' that have tended to be designed for best legibility on the Windows GDI render engine.

Then, ironically, it was used by G. Michaels Consulting Ltd. as a font purely for Windows, modified to have slashes on the zeroes.

## License

The Dbdoczygen Fonts are released under either The SIL Open Font License (OFL) version 1.1 or the GNU General Public License version 3 with font exception (GPL+FE).

Copyright 2011-2013 Vernon Adams <vern@newtypography.co.uk>
Copyright 2018 Keith Zubot-Gephart / G. Michaels Consulting Ltd. <keith@gmcl.com>
