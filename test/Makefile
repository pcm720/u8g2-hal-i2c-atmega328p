
PRJ = u8g2_test
MCU = atmega328p
CLK = 16000000UL

SRC = $(PRJ).c

CFLAGS  = -Os -mmcu=$(MCU) -DF_CPU=$(CLK) -Wall
CFILES    = $(PRJ).c

PRG = apu2 -P ft0
AVRDUDE = taskset -c 1 avrdude -c $(PRG) -p $(MCU) -C ~/.avrduderc -C /etc/avrdude.conf
LFU = 0xFF
HFU = 0xDF
EFU = 0x05

OBJCOPY = avr-objcopy
OBJDUMP = avr-objdump
SIZE    = avr-size --format=avr --mcu=$(MCU)
CC      = avr-gcc

all: $(PRJ).hex

clean:
	rm -f *.hex *.elf *.o

test:
	$(AVRDUDE) -v

flash: all
	$(AVRDUDE) -U flash:w:$(PRJ).hex:i

fuse:
	$(AVRDUDE) -U lfuse:w:$(LFU):m -U hfuse:w:$(HFU):m -U efuse:w:$(EFU):m

disasm: $(PRJ).elf
	$(OBJDUMP) -d $(PRJ).elf

$(PRJ).elf:
	$(CC) $(CFLAGS) -c $(PRJ).c -o $(PRJ).o
	$(CC) -mmcu=$(MCU) $(PRJ).o -o $(PRJ).elf

$(PRJ).hex: $(PRJ).elf
	rm -f $(PRJ).hex
	$(OBJCOPY) -j .text -j .data -O ihex $(PRJ).elf $(PRJ).hex
	$(SIZE) $(PRJ).elf