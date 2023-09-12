# Wireshark channelBWs Parser
online calculator: https://dustinchen26.github.io/bw_wireshark

## Usage
● Usage: Parse Wireshark UeCapabilityInformation NR supported channelBWs
```
> ref: 3GPP spec ETSI TS 138 306
> (Rule1) => For FR1, the bits in channelBWs-DL starting from the leftmost bit indicate 5, 10, 15, 20, 25, 30, 40, 50, 60 and 80MHz. ex: channelBWs-DL fr1 :{scs-30kHz '00010111 11'B},
> (Rule2) => For FR1, the leading/leftmost bit in channelBWs-DL-v1590 indicates 70MHz, and all the remaining bits in channelBWs-DL-v1590 shall be set to 0. ex:{scs-30kHz '10000000 00000000'B},
> (Rule3) => To determine whether the UE supports a channel bandwidth of 90 MHz, the network may ignore this capability for and validate instead the channelBW-90mhz and the supportedBandwidthCombinationSet. ex: channelBW-90mhz supported,
> (Rule4) => whether the UE supports a channel bandwidth of 100 MHz, ex: supportedBandwidthDL fr1 : mhz100
> ex: Compal UE mifi n78 SCS=30 support BW 20, 30, 40, 50, 60, 70, 80, 90, 100
```

## Example input
● Open f1_tcp.pcap with Wireshark, search for "supportedBandListNR", right-click "Expand Subtrees", right-click "Copy->All Visiable Selected Tree Items", paste it below, and parse
```
bandNR: 48
channelBWs-DL: fr1 (0)
    fr1
        scs-15kHz: 0000 [bit length 10, 6 LSB pad bits, 0000 0000  00.. .... decimal value 0]
        scs-30kHz: 73c0 [bit length 10, 6 LSB pad bits, 0111 0011  11.. .... decimal value 463]
        scs-60kHz: 0000 [bit length 10, 6 LSB pad bits, 0000 0000  00.. .... decimal value 0]
channelBWs-UL: fr1 (0)
    fr1
        scs-15kHz: 0000 [bit length 10, 6 LSB pad bits, 0000 0000  00.. .... decimal value 0]
        scs-30kHz: 73c0 [bit length 10, 6 LSB pad bits, 0111 0011  11.. .... decimal value 463]
        scs-60kHz: 0000 [bit length 10, 6 LSB pad bits, 0000 0000  00.. .... decimal value 0]
pucch-SpatialRelInfoMAC-CE: supported (0)
```

## Output
```
bandNR: 48
channelBWs-DL
    scs-15kHz: 0000000000 Supported Bandwidths (scs-15kHz):  MHz
    scs-30kHz: 0111001111 Supported Bandwidths (scs-30kHz): 10, 15, 20, 40, 50, 60, 80 MHz
    scs-60kHz: 0000000000 Supported Bandwidths (scs-60kHz):  MHz
channelBWs-UL
    scs-15kHz: 0000000000 Supported Bandwidths (scs-15kHz):  MHz
    scs-30kHz: 0111001111 Supported Bandwidths (scs-30kHz): 10, 15, 20, 40, 50, 60, 80 MHz
    scs-60kHz: 0000000000 Supported Bandwidths (scs-60kHz):  MHz
```