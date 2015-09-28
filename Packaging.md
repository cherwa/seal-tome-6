**Table of Contents**


---





---


#summary Packaging

# Introduction #
<a href='http://imgur.com/tE4Jak0'><img src='http://i.imgur.com/tE4Jak0.png?1' align='right' title='Hosted by imgur.com' /></a>
> The spell tome has five separate spells, each of which has its corresponding page in the tome. To activate the spell, the user must simply open to the corresponding page. The goal is to accurately detect which page the user turned to. We will do this by using a series of phototransistors which will allow or restrict current flowing to the pins based on which page is currently open. Each phototransistor will be supplied a voltage and will have its own pin on the PIC. The idea is that when the book is closed, the phototransistors will not be receiving light and would not allow current to flow. When the user flips to a page, the corresponding phototransistor will be exposed to light. This would allow current to flow through the phototransistor and be detected by the pin.

> For packaging, we want the enclosure to look as much as book as possible. For this we will hollow out a book and embed all our components within. The page flipping mechanism only requires a few pages, thus the majority of the book space will be used to house the components and will be kept sealed and out of sight.

> For the visual component of our project, our plan is to shine RGB LEDs through an acrylic sheet that's bound to the book cover. Depending on power constraints, we might to this on the back book cover as well.<br />

## Outputs / Layout ##
<a href='http://imgur.com/aiFtO4C'><img src='http://i.imgur.com/aiFtO4C.png?1' align='right' title='Phototransistor layout' /></a>
| PT[4:0] (Binary) | Outcome |
|:-----------------|:--------|
| 00000            | Book is Closed |
| 00001            | Open to page 1 |
| 00011            | Open to page 2 |
| 00111            | Open to page 3 |
| 01111            | Open to page 4 |
| 11111            | Open to page 5 |
| XXXXX any other  | Treat as closed |

## Flowchart ##
<a href='http://imgur.com/qzzYwsD'><img src='http://i.imgur.com/qzzYwsD.png' title='Hosted by imgur.com' /></a><a href='http://imgur.com/tE4Jak0'>
<hr />
<h1>Research</h1>

<blockquote>Because each spell would require its own pin on the PIC, it was important acquire a microcontroller with enough pins to support everyone’s block. Once an appropriate microcontroller was selected, it was important to find phototransistors with very small dimensions. Because we have to make the phototransistors fit in between pages on the book, we wanted ones with the shortest height so that the book looks normal when closed. The specs on each of the transistors were for the most part identical, the only trait that seemed to change was the viewing angle, but we feel that for this application, the viewing angle isn’t that important.<br /></blockquote>

<h2>Phototransistor Choice 1:</h2>
<a href='http://imgur.com/aK2Qqmo'><img src='http://i.imgur.com/aK2Qqmo.png?1' align='right' title='Hosted by imgur.com' /></a>
<blockquote>The first choice, the BPW17N, is an NPN phototransistor with a flat lens. The smaller dimensions and form factor was a better choice over the dome lens variety of phototransistors.  At a height of 2.2mm we felt that this was sufficiently small for our purposes.</blockquote>

<a href='http://www.mouser.com/ds/2/427/bpw16n-109596.pdf'>BPW17N Datasheet</a>

<h2>Phototransistor Choice 2:</h2>
<a href='http://imgur.com/kYlr9Tj'><img src='http://i.imgur.com/kYlr9Tj.png?1' align='right' title='Hosted by imgur.com' /></a>
<blockquote>The second choice is a surface mount dome window phototransistor, the VEMT2503X01. This was our second choice because even though it’s of the dome lens type, it is still only 2.55mm in height. If we couldn’t work with our first choice, this would be a good backup.</blockquote>

<a href='http://www.mouser.com/ds/2/427/vemt2503x01-256525.pdf'>VEMT2503X01 Datasheet</a>

<h2>Phototransistor Choice 3:</h2>
<a href='http://imgur.com/uTaxKOz'><img src='http://i.imgur.com/uTaxKOz.png?1' align='right' title='Hosted by imgur.com' /></a>
<blockquote>The third choice we would only consider if the first two fail completely. Our last choice would be the BPW85, a through-hole, dome lens phototransistor. Because the height is a lot bigger than our first two choices (4.5mm), it would be more difficult to package and we would only consider it as a last resort.</blockquote>

<a href='http://www.mouser.com/ds/2/427/bpw85-266683.pdf'>BPW85 Datasheet</a>

<h2>Alternate Component Choice:</h2>
<a href='http://imgur.com/KKCbLBc'><img src='http://i.imgur.com/KKCbLBc.png?1' align='right' title='Hosted by imgur.com' /></a>
<blockquote>Instead of a lone phototransistor, it might be possible to use a slotted optical switch like the TCST1103. The benefit of using this kind of switch is that it provides its own light source and has a daylight blocking filter. This means that all we would need to do to make the switch, is to put something into the slot, essentially breaking the built in phototransistors light source. The negative is the size. These components are much larger than the lone phototransistors and would complicate packaging.</blockquote>

<a href='http://www.mouser.com/ds/2/427/tcst1103-240313.pdf'>TCST1103 Datasheet</a>

<hr />
<h1>Phototransistors</h1>

<blockquote>Listed below are the different phototransistors (listed from worst to best) that were considered for the spell tome’s page detector. Because our battery will never provide us with more than 5V, breakdown voltage wasn’t a factor. Because the prices, fall/rise times, and power dissipations were all very similar, the factors that affected the decision the most were the dimensions.<br /></blockquote>

<table><thead><th> Phototransistors </th><th> Collector-Emitter Saturation Voltage (V) </th><th> Collector-Emitter Saturation Voltage (V) </th><th> Collector Peak Current (mA) </th><th> Fall Time (μs) </th><th> Rise Time (μs) </th><th> Maximum Power Dissipation (mW) </th><th> Cost </th></thead><tbody>
<tr><td> BPW85            </td><td> 70                                       </td><td> .3                                       </td><td> 100                         </td><td> 2.3            </td><td> 2              </td><td> 100                            </td><td> $0.67 </td></tr>
<tr><td> VEMT2503X01      </td><td> 20                                       </td><td> .4                                       </td><td> 100                         </td><td> 8              </td><td> 4.5            </td><td> 100                            </td><td> $0.57 </td></tr>
<tr><td> BPW17N           </td><td> 32                                       </td><td> .3                                       </td><td> 100                         </td><td> 5              </td><td> 4.8            </td><td> 100                            </td><td> $0.74 </td></tr></tbody></table>

<h1>Optical Switches</h1>

<blockquote>Listed below are a couple of optical switches that we would consider if using lone phototransistors were to fail. Because these are larger in dimension (10-15mm in height), we would prefer to avoid using them, but are still a viable option should phototransistors fail.<br /></blockquote>

<table><thead><th> Optical Switch (Detector) </th><th> Collector-Emitter Saturation Voltage (V) </th><th> Collector-Emitter Saturation Voltage (V) </th><th> Collector Peak Current (mA) </th><th> Fall Time (μs) </th><th> Rise Time (μs) </th><th> Maximum Power Dissipation (mW) </th><th> Cost </th></thead><tbody>
<tr><td> TCST1103                  </td><td> 70                                       </td><td> .4                                       </td><td> 200                         </td><td> 8              </td><td> 10             </td><td> 100                            </td><td> $1.30 </td></tr>
<tr><td> SFH9500                   </td><td> 30                                       </td><td> .4                                       </td><td> 50                          </td><td> 17             </td><td> 13             </td><td> 100                            </td><td> $0.90 </td></tr></tbody></table>

<hr />
<hr />

<hr />
<a href='MainPage.md'>Home</a>

<a href='Research.md'>Research Home</a>

<a href='prototype.md'>Prototype Home</a>

<a href='Integration.md'>Integration Phase I Home</a>