# Oxygen GMCL Font

Oxygen Font is a project to design a desktop/gui font for integrated
use with the KDE desktop.

The basic concept for Oxygen Font is to design a clear, legible, sans
serif font which would be rendered with Freetype on Linux-based
devices. In addition a bold weight, plus regular and bold italics, and
a monospace version will be made.

G. Michaels Consulting Ltd. then wanted slashes on the zeroes, and so
here we are!

## Requirements

You'll need at least FontForge, as well as `eot-utils` (that's the *buntu
package, at least) for the EOT output.

## Design

Oxygen is to be constructed closely with the gridfitting aspects of
the Freetype engine. The Oxygen fonts will also be autohinted with
Werner Lemberg's "ttfautohint" library to further the compatibility
with the Freetype engine. The aim of this approach is to produce a
family of freetype-specific desktop fonts whose appearance will stay
uniform under different screen render settings, unlike more
traditionally designed 'screen fonts' that have tended to be designed
for best legibility on the Windows GDI render engine.

Then, ironically, it was used by G. Michaels Consulting Ltd. as a font
purely for Windows, modified to have slashes on the zeroes.

## License

The Oxygen Fonts are released under either The SIL Open Font License
(OFL) version 1.1 or the GNU General Public License version 3 with
font exception (GPL+FE).

Copyright 2011-2013 Vernon Adams <vern@newtypography.co.uk>
Copyright 2018 Keith Zubot-Gephart <keith@gmcl.com>
