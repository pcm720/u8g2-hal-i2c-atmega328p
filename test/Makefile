
PRJ = u8g2_test
MCU = atmega328p
CLK = 16000000

SRC = $(PRJ).c

CFLAGS    = -Wall -Os -DF_CPU=$(CLK) -mmcu=$(MCU) $(INCLUDE)
CFILES    = $(PRJ).c

OBJCOPY = avr-objcopy
OBJDUMP = avr-objdump
SIZE    = avr-size --format=avr --mcu=$(MCU)
CC      = avr-gcc

all: $(PRJ).hex

clean:
	rm -f *.hex *.elf *.o

$(PRJ).elf:
	$(CC) $(CFLAGS) -c $(PRJ).c -o $(PRJ).elf

$(PRJ).hex: $(PRJ).elf
	rm -f $(PRJ).hex
	$(OBJCOPY) -j .text -j .data -O ihex $(PRJ).elf $(PRJ).hex
	$(SIZE) $(PRJ).elf