# Checksums

## What are checksums and what are they useful for?

Checksums are value calculated on a set of data to make sure the integrity of the data when its transmitted or stored in memory.

They are useful when you want to send a message over a communication protocol. Checksum value can be sent before or after the actual data. A CRC is a type of checksum that is widely used.

> typedef PACKED_STRUCT
> {
>    //   The number of bytes in the message.
>    uint16_t length;
>    //   The CRC16 of all bytes in the message.
>    uint16_t crc16;
>    //   The message...  Set to maximum possible encoded size.
>    uint8_t message[252];
> } sample_message_t;

Checksum can also be used to validate an image before updating during an OTA. A simple process of OTA with checksum would look something like this
 - Generate a binary image that can be sent for OTA update.
 - Compute the checksum/CRC of the binary image
 - Either send the checksum/CRC value separately or append it to the binary image.
 - Download the binary image on the device
 - Compute the checksum/CRC of the received binary on the device.
 - Validate the checksum/CRC matches the received/stored checkssum/CRC values.
 - Proceed with updating the new binary image on device.