# OnethinxCoreAPI_Extended
Extended Stack API for low-level LoRa communication on the Onethinx Core

These API functions allow to communicate with the SX1261 and SX1262 directly. 

**Example**

Initialization:

```
uint8_t TXdata[] = "Hello world";
uint8_t RXdata[15];

RadioStatus_t RadioStatus;

LoRaParams_t LoRaParams =
{
	.Frequency = 9030000,           // Frequency in steps of 100Hz
	.TXpower = PWR_MAX,
	.Modulation.SF = LORA_SF7,
	.Modulation.BW = LORA_BW_250,
	.Modulation.CR = LORA_CR_4_5,
	.Modulation.LowDataRateOptimize = LORA_LOWDATARATEOPTIMIZE_OFF,
	.Packet.PreambleLength = 8,
	.Packet.HeaderType = LORA_PACKET_VARIABLE_LENGTH,
	.Packet.PayloadSize = 15,
	.Packet.CRCmode = LORA_CRC_ON,
	.Packet.IQmode = LORA_IQ_NORMAL,
	.Packet.SyncWord = LORA_MAC_PUBLIC_SYNCWORD
};
```
Unlock the stack* for use of the extended library functions:
```
LoRaWAN_Unlock();
```

Sending data over LoRa:
```
LoRa_TX(&LoRaParams, &RadioStatus, (uint8_t *) &TXdata, sizeof(TXdata), 3000);
```

Receiving data:
```
LoRa_RX(&LoRaParams, &RadioStatus, (uint8_t *) &RXdata, sizeof(RXdata), 30000);
```


*Caution: use of these functions voids LoRa Alliance Certification by Similarity.

