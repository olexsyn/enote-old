# Keyboard

`/usr/share/X11/xkb/symbols/ua`

```xml
default  partial alphanumeric_keys
xkb_symbols "unicode" {

    include "ua(winkeys)"
    name[Group1]= "Ukrainian";

    key <TLDE> { [      apostrophe,      asciitilde,              U2019,           U0301  ] };  // Apostrophe and Stress symbol
    key <AE01> { [               1,          exclam,        onesuperior                   ] };
    key <AE02> { [               2,        quotedbl,        twosuperior                   ] };
    key <AE03> { [               3,      numbersign,         numerosign,           U20B4  ] };  // Paragraph and Hryvnia sign
    key <AE04> { [               4,       semicolon,             dollar,        EuroSign  ] };
    key <AE05> { [               5,         percent,             degree                   ] };
    key <AE06> { [               6,           colon,               less                   ] };
    key <AE07> { [               7,        question,            greater                   ] };
    key <AE08> { [               8,        asterisk, enfilledcircbullet                   ] };
    key <AE09> { [               9,       parenleft,        bracketleft,       braceleft  ] };
    key <AE10> { [               0,      parenright,       bracketright,      braceright  ] };
    key <AE11> { [           minus,      underscore,             emdash,          endash  ] };
    key <AE12> { [           equal,            plus,           notequal,       plusminus  ] };

    key <AD03> { [      Cyrillic_u,          Cyrillic_U,       Byelorussian_shortu,       Byelorussian_SHORTU  ] };
    key <AD04> { [     Cyrillic_ka,         Cyrillic_KA,                registered                             ] };  // Registered tm
    key <AD05> { [     Cyrillic_ie,         Cyrillic_IE,               Cyrillic_io,               Cyrillic_IO  ] };  // е / ё
    key <AD07> { [    Cyrillic_ghe,        Cyrillic_GHE, Ukrainian_ghe_with_upturn, Ukrainian_GHE_WITH_UPTURN  ] };  // г / ґ
    key <AD12> { [    Ukrainian_yi,        Ukrainian_YI,         Cyrillic_hardsign,         Cyrillic_HARDSIGN  ] };  // ї / ъ
    key <AC02> { [     Ukrainian_i,         Ukrainian_I,             Cyrillic_yeru,             Cyrillic_YERU  ] };  // і / ы
    key <AC11> { [    Ukrainian_ie,        Ukrainian_IE,                Cyrillic_e,                Cyrillic_E  ] };  // є / э

    key <BKSL> { [           slash,             bar,     backslash                        ] };

    key <AB03> { [     Cyrillic_es,     Cyrillic_ES,      copyright                       ] };
    key <AB06> { [     Cyrillic_te,     Cyrillic_TE,      trademark                       ] };
    key <AB08> { [     Cyrillic_be,     Cyrillic_BE,  guillemotleft,  doublelowquotemark  ] };
    key <AB09> { [     Cyrillic_yu,     Cyrillic_YU, guillemotright, leftdoublequotemark  ] };
    key <AB10> { [          period,           comma,          slash,            ellipsis  ] };

    include "level3(ralt_switch)"
};
```
