# OPEN LETTER TO GUSTAVO FRANCO

[Português](README.md) / [English](README.en.md) / [Español](README.es.md) / [Italiano](README.it.md) / [Deutsch](README.de.md) / [简体中文](README.zh-CN.md) / [日本語](README.ja.md) / [繁體中文（香港）](README.zh-HK.md)

Request for clarification, correction of attribution, and public retraction
November 11, 2026

Gustavo,

I created this fork after you archived the repository because it was the only quick and direct way I found to try to get this letter to you as soon as possible.

I am writing to dispute the attribution published in your repository, which identifies the cartridges mentioned on that page as a commercialization of your implementation of Street Fighter Alpha 2 without the S-DD1.

My statement about the origin of the edition is explicit: I did not use material from your project in the 8 MiB USA edition with Shin Akuma and accelerated loading that I supplied through my decompression work and patches prepared for 29LV640 memory. I state that the cartridges I am referring to use that edition. I dispute attributing those cartridges to your project without technically identifying the content actually used.

The purpose of this letter is to clarify the origin of the edition concerned, explain the development of my work, and request that the public attribution be supported by verifiable evidence.

## 1. THE DEVELOPMENT OF MY PROJECT

My work did not begin when I made the 8 MiB patches available. There was an earlier process of studying the S-DD1, developing tools, analyzing the memory mapping, assembling boards, implementing corrections, and testing on a real SNES.

The original plan involved a PCB with a CPLD to control access to the data and preserve the implementation details. I did not intend to make the entire decompression, data organization, and reconstruction system openly available.

When I learned that your project had been published, I became deeply discouraged. I felt that the distinguishing value of the work in which I had invested time and effort had been compromised. That was my perception of my project's future.

It was in that context that I decided to change direction and privately make the decompression work and patches for the 8 MiB edition available, so that the work already undertaken could continue. That decision does not justify automatically identifying the edition I supplied as a version from your repository.

## 2. HOW MY DECOMPRESSION APPROACH WORKS

In the original sdd1_unpacker core, I studied and isolated the S-DD1 implementation in bsnes. The code credits were preserved: Andreas Naive for the original algorithm/implementation and byuu for the bsnes port. I do not claim to have invented the S-DD1 algorithm.

That code was adapted into a C++ tool independent of the graphical interface and the full emulator execution loop, with validated ROM reads and handling of the S-DD1 memory banks.

The game does not treat the entire ROM as a single compressed file. It requests specific streams, usually during DMA transfers. The work therefore involved analyzing descriptors and tables in the original ROM, recording requests made during execution, and consolidating source addresses, lengths, and memory-bank configurations.

The canonical trace for the historical reconstruction contains 3,155 request identities across 3,160 lines. The five additional lines record evidence from other call sites for requests already cataloged. Observed requests and statically inferred entries are classified separately; this count does not mean 3,155 distinct compressed streams or, by itself, prove coverage of every possible situation in the game.

The original core's pipeline was structured as: original USA ROM, analysis and traces, request catalog, data decompression, organization into a new layout, DMA patches, and verification of the S-DD1-free reconstruction.

That reconstruction required distinguishing CPU addresses from file offsets, respecting the SNES ROM address regions, and redirecting the relevant routines to already-decompressed data. It is not merely a matter of enlarging the file or changing its header.

## 3. THE 8 MiB ADAPTATION AND THE SIMPLE BOARD

The 8 MiB line must be distinguished from the earlier 16 MiB reconstruction core. It underwent a separate organization and allocation process, using an inventory extracted from the 16 MB base that I tested and demonstrated on YouTube, together with subsequent corrections and checks. I am not presenting it as a simple truncation of the 16 MiB file.

The edition was prepared for a simple board with the appropriate connections and a single 8 MiB TSOP48 Flash memory device, the 29LV640 in x8 mode. This edition does not require an S-DD1 or CPLD to operate in that configuration and has been tested on a real SNES. A variant for a modified LoROM board was also prepared.

There is an objective difference from the historical 12 MiB conversion documented in your project. That 12 MiB image cannot simply be programmed into an 8 MiB 29LV640 and used in the configuration I demonstrated. Your own technical account describes a specific mapping, including a window in banks C0-FF:

https://github.com/snes9xgit/snes9x/issues/1081

I am not claiming that your implementation could never be adapted to a physical cartridge, nor am I denying the hardware tests you documented. I am distinguishing a 12 MiB image and its mapping from the 8 MiB edition prepared for my board configuration.

If the aim is to broaden access to the game, I believe this approach should also be recognized: allowing people to use a simple board and accessible components without needing to purchase a specific flashcart. I had already recorded a test board used in this work; the video is included in the list at the end of this letter.

## 4. CREDITS AND ACCURACY

This dispute concerns specifically the 8 MiB USA edition used in the cartridges mentioned. The origin of that edition must be examined using the files actually used, their patches, and their provenance. It should not be presumed from inventories for another region or separate research revisions, nor merely from similarities between the advertised features.

I do not claim exclusive authorship of the public algorithm, third-party routines, or the original game's data. I ask for accurate recognition of the integration, adaptation, correction, and validation work carried out for the edition I supplied.

## 5. PUBLIC RECORDS FOR CHECKING THE TIMELINE

I provide the following records so that their content and publication dates can be checked against the version history. They document the development I am describing; they do not replace comparison of the files actually used in the cartridge.

Simple test board:
https://www.youtube.com/shorts/EVQoQB8mD1A

Additional record 1:
https://www.youtube.com/shorts/uhzHfQFPbVw

Additional record 2:
https://www.youtube.com/shorts/23gS_IEGDqc

Project-related livestream:
https://www.youtube.com/live/zakojPNeGc0

Additional record 3:
https://www.youtube.com/shorts/PXVAKPfAO1E

Additional record 4:
https://www.youtube.com/shorts/y8PAzIzPz1I

Additional record 5:
https://www.youtube.com/shorts/bStb8AW_QzQ

Additional record 6:
https://www.youtube.com/shorts/if26BECUllI

PCB and CPLD stage:
https://www.youtube.com/shorts/X-Hby6Vw-m4

Video I published before preparing and privately sharing the 8 MiB patches:
https://www.youtube.com/shorts/YZbpycbEW0w

Later demonstration of the game on a simple board with the 29LV640:
https://www.youtube.com/shorts/GKl1eOMFks0

My clarification addressed to you:
https://youtu.be/8X8jRSXFb5I

## 6. WHAT I AM REQUESTING

The publication I am referring to is located at:
https://github.com/gufranco/snes-street-fighter-alpha-2-nochip

I request that you explain which file was examined, its hash, which cartridge it was obtained from, and what technical evidence supported attributing it to your implementation.

I also request that the comparison consider the physical mapping, routines, patches, and specific revision rather than treating the commercial description or features such as Shin Akuma and accelerated loading as sufficient proof.

While that identification remains disputed and no technical demonstration has been presented, I ask that the publication make that situation explicit and remove the categorical attribution. If the attribution is confirmed to be mistaken, I request that the publications be corrected and that a public retraction receive visibility equivalent to the original exposure.

I respect your work and ask that you respect mine as well. I do not intend to encourage personal attacks or diminish your dedication.

The issue I am raising is specific: the origin of an implementation must be demonstrated. A similar result, a listing title, or packaging does not replace analysis of the content actually used.

Sincerely,

The person responsible for the ALBER MULTI HOUSE project
