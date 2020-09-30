# steezy
Steezy is a python tool for ghetto generation of Yara rules from the VA
of a function in a compiled executable.

## Installation
* Install dependancies.
* Clone git repo.
* Hope it works.

### Dependancies
Python 3.x (Tested with 3.7+).

https://www.capstone-engine.org/

https://github.com/fox-it/mkyara

https://github.com/radareorg/radare2

https://github.com/radareorg/radare2-r2pipe

## Usage

```
$ ./steezy.py -f ~/MALWARE/5d59311fc5407d55c96016dbc4e72006 -o 0x10001e20

rule steezy_5d59311fc5407d55c96016dbc4e72006 {

    meta:
        author = "Steezy"
        md5 = "5d59311fc5407d55c96016dbc4e72006"

    strings:

        // Function Virtual Address: 0x10001e20
        $r2_static_0x10001e20 = { 55 8b ec 83 ec 10 e8 05 fa ff ff c7 45 fc 00 00 00 00 8d 45 fc 50 e8 f5 f8 ff ff 50 e8 7f f7 ff ff 89 45 f0 83 7d fc 01 75 0e e8 b1 73 00 00 6a 00 e8 6a f8 ff ff eb 46 83 7d fc 02 75 40 e8 ad a7 00 00 89 45 f8 8b 4d f8 51 6a 00 6a 00 e8 dd f7 ff ff 89 45 f4 e8 25 f9 ff ff 3d b7 00 00 00 75 07 6a 00 e8 37 f8 ff ff e8 22 fa ff ff 6a 00 e8 db fd ff ff 8b 55 f4 52 e8 62 f1 ff ff e8 6d f9 ff ff 33 c0 8b e5 5d c3 }
        $r2_wildcard_0x10001e20 = {558bec83ec10e8????????c745fc????????8d45fc50e8????????50e8????????8945f0837dfc0175??e8????????6a??e8????????eb??837dfc0275??e8????????8945f88b4df8516a??6a??e8????????8945f4e8????????3d????????75??6a??e8????????e8????????6a??e8????????8b55f452e8????????e8????????33c08be55dc3}
        $r2_blocks_0x10001e20 = {558bec83ec10e8????????c745fc????????8d45fc50e8????????50e8????????8945f0837dfc01[2-6]e8????????6a??e8????????[2-6]837dfc02[2-6]e8????????8945f88b4df8516a??6a??e8????????8945f4e8????????3d????????[2-6]6a??e8????????e8????????6a??e8????????8b55f452e8????????e8????????33c08be55dc3}
        $mkyara_0x10001e20 = { 55 8B EC 83 EC 10 E8 ?? ?? ?? ?? C7 45 ?? 00 00 00 00 8D 45 ?? 50 E8 ?? ?? ?? ?? 50 E8 ?? ?? ?? ?? 89 45 ?? 83 7D ?? 01 75 ?? E8 ?? ?? ?? ?? 6A 00 E8 ?? ?? ?? ?? EB ?? 83 7D ?? 02 75 ?? E8 ?? ?? ?? ?? 89 45 ?? 8B 4D ?? 51 6A 00 6A 00 E8 ?? ?? ?? ?? 89 45 ?? E8 ?? ?? ?? ?? 3D B7 00 00 00 75 ?? 6A 00 E8 ?? ?? ?? ?? E8 ?? ?? ?? ?? 6A 00 E8 ?? ?? ?? ?? 8B 55 ?? 52 E8 ?? ?? ?? ?? E8 ?? ?? ?? ?? 33 C0 8B E5 5D C3}

    condition:
        any of them
}
```

Steezy will generate four rules:

* Rule with static bytes, not so useful.
* Rule with Yara wildcards using r2's instruction mask.
* Rule with Yara wildcards using r2's instruction mask and Yara ranges based around function blocks.
* Rule generated with Fox-It mkYARA.

## Additional Resources
Some other tools I've used for generating Yara rules which lead me to creating
my own.

https://gist.github.com/williballenthin/3abc9577bede0aeef25526b201732246

https://github.com/fxb-cocacoding/yara-signator

https://github.com/TcM1911/zig2yar

https://github.com/mrexodia/YaraGen

https://github.com/immortalp0ny/yarg

https://github.com/arieljt/VTCodeSimilarity-YaraGen

https://github.com/lucamassarelli/yarasafe

https://github.com/fox-it/mkyara

